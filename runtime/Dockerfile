# Build context: the workspace root containing araru-server and araru-web.
# Example from a sibling workspace: docker build -f araruoss/runtime/Dockerfile --target server .

FROM node:22-alpine AS server
RUN apk add --no-cache p7zip poppler-utils
WORKDIR /app
COPY araru-server/package.json araru-server/package-lock.json ./
RUN npm ci --omit=dev
COPY araru-server/server ./server
COPY araru-server/scripts ./scripts
RUN mkdir -p /app/storage && chown -R node:node /app
ENV NODE_ENV=production
USER node
EXPOSE 3001
HEALTHCHECK --interval=30s --timeout=5s --start-period=20s --retries=3 \
  CMD node -e "fetch('http://127.0.0.1:3001/ready').then(r=>{if(!r.ok)process.exit(1)}).catch(()=>process.exit(1))"
CMD ["npm", "start"]

FROM node:22-alpine AS web-build
WORKDIR /app
COPY araru-web/package.json araru-web/package-lock.json ./
RUN npm ci
COPY araru-web/ ./
ARG VITE_API_URL=/api/v1
ENV VITE_API_URL=${VITE_API_URL}
RUN npm run build

FROM nginx:1.27-alpine AS web
COPY araru-web/nginx.conf.template /etc/nginx/templates/default.conf.template
COPY --from=web-build /app/dist /usr/share/nginx/html
ENV API_UPSTREAM=http://server:3001
ENV CSP_CONNECT_SRC=""
EXPOSE 80
HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
  CMD wget -q -O /dev/null http://127.0.0.1/healthz || exit 1
