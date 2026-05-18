# ============================================================
# Dockerfile — OpenClaw Red Hat Presentation
# 
# Imagem leve non-root para servir a apresentação HTML no OpenShift
# Compatível com SecurityContextConstraints padrão (runAsNonRoot: true)
# ============================================================

FROM nginxinc/nginx-unprivileged:alpine

# Remove config padrão e cria uma configuração limpa
RUN rm /etc/nginx/conf.d/default.conf

# Configuração customizada do nginx
RUN echo 'server { \
    listen 8080; \
    root /usr/share/nginx/html; \
    index index.html; \
    location / { \
        try_files $uri $uri/ /index.html; \
    } \
}' > /etc/nginx/conf.d/presentation.conf

# Copia a apresentação
COPY index.html /usr/share/nginx/html/index.html

# Porta 8080 = OpenShift friendly (non-root)
EXPOSE 8080

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD wget -qO- http://localhost:8080/ || exit 1

CMD ["nginx", "-g", "daemon off;"]
