# 🌐 colomr.dev

¡Hola! Este es el repositorio de mi landing page personal. Está construida con HUGO Framework y desplegada en Firebase. La uso como punto central para compartir mis redes sociales y mi trayectoria profesional. 👋

## 🛠️ Tecnologías

- [HUGO](https://gohugo.io/) - Framework para sitios web estáticos
- [Firebase](https://firebase.google.com/) - Plataforma de hosting
- [Google Cloud Platform](https://cloud.google.com/) - Para pruebas y experimentos

## 🚀 Despliegue en Firebase

Para desplegar el sitio en Firebase, sigue estos pasos:

1. Instala la CLI de Firebase:
```bash
npm install -g firebase-tools
```

2. Inicia sesión en Firebase:
```bash
firebase login
```

3. Inicializa Firebase en el directorio raíz de Hugo:
```bash
firebase init
```

4. Durante la inicialización:
   - ✅ Selecciona la funcionalidad **Hosting**
   - ✅ Elige tu proyecto de Firebase
   - ✅ Acepta el valor predeterminado para reglas de base de datos
   - ✅ Usa `public` como directorio de publicación
   - ❌ Responde "No" a la aplicación de una sola página

5. Despliega el sitio:
```bash
firebase deploy --only hosting
```

## 🔍 Más Información

Para conocer más sobre mi trayectoria profesional y contactar conmigo, ¡visita [colomr.pm](https://colomr.pm)! 🌟
