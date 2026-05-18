# 🎯 Navi's Apresentações

Repositório central de apresentações sobre **OpenClaw**, criadas pela **Navi** para o Luciano.

## 📂 Estrutura

```
apresentacao-openclaw-redhat/
├── index.html     → Apresentação completa (20 slides + 5 executivos)
├── Dockerfile     → Container non-root para OpenShift
└── deploy.yaml    → Deployment + Service + Route para OpenShift
```

## 🚀 Deploy no OpenShift

```bash
# Build
oc new-build --name navi-apresentacao-openclaw --binary -l app=navi-apresentacao
oc start-build navi-apresentacao-openclaw --from-dir=apresentacao-openclaw-redhat/ --follow

# Deploy
oc apply -f apresentacao-openclaw-redhat/deploy.yaml

# Ou construindo direto:
podman build -t navi-apresentacao-openclaw apresentacao-openclaw-redhat/
```

## 📖 Apresentações

| Pasta | Descrição | Slides |
|-------|-----------|--------|
| `apresentacao-openclaw-redhat/` | OpenClaw: A Nova Fronteira dos Agentes de IA (tema Red Hat) | 20 + 5 executivos |

---

_Criado por Navi 🔮 para Luciano_
