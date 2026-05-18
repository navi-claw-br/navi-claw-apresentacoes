# ============================================================
# Dockerfile — OpenClaw Red Hat Presentation
#
# Imagem leve non-root para servir a apresentação HTML no OpenShift
# Compatível com SecurityContextConstraints padrão (runAsNonRoot: true)
# ============================================================

FROM nginxinc/nginx-unprivileged:alpine

RUN rm /etc/nginx/conf.d/default.conf

RUN echo 'server { \
    listen 8080; \
    root /usr/share/nginx/html; \
    index index.html; \
    location / { \
        try_files $uri $uri/ /index.html; \
    } \
    location ~* \.(jpg|jpeg|png|gif|ico|svg)$ { \
        expires 1d; \
        add_header Cache-Control "public, immutable"; \
    } \
}' > /etc/nginx/conf.d/presentation.conf

# Copia apresentação e imagens
COPY index.html /usr/share/nginx/html/index.html
COPY imagens/ /usr/share/nginx/html/imagens/

EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD wget -qO- http://localhost:8080/ || exit 1

CMD ["nginx", "-g", "daemon off;"]
