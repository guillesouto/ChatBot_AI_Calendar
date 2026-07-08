# AI Calendar Assistant - Prueba Técnica Fusuma

Asistente de calendario inteligente en tiempo real que permite gestionar eventos de Google Calendar mediante lenguaje natural utilizando el modelo Gemini a través de técnicas de Tool Calling asistido.

## 🏗️ Arquitectura y Decisiones Técnicas

### 1. Framework & Rendering: Next.js (App Router)
Se seleccionó Next.js por su capacidad nativa para manejar rutas de API eficientes junto con componentes de servidor y cliente híbridos, minimizando el JS enviado al navegador y permitiendo un manejo seguro de secrets en el backend.

### 2. Capa de Inteligencia Artificial: Vercel AI SDK + Gemini
* **Vercel AI SDK (`ai`):** Se utilizó para gestionar flujos de streaming de texto (`streamText`) en tiempo real hacia la interfaz, reduciendo la percepción de latencia del modelo (Time to First Token).
* **Gemini Pro:** Configurado como motor cognitivo debido a su alto rendimiento nativo en arquitecturas de **Tool Calling (Llamada a herramientas)**, interpretando las intenciones del usuario ("Agenda algo mañana...") y estructurando parámetros JSON exactos requeridos por la API de Google.

### 3. Autenticación y Flujo OAuth: NextAuth.js
Para interactuar de manera segura con el entorno personal del usuario, se implementó un flujo completo de autenticación OAuth 2.0 con Google. Los tokens (`access_token` para peticiones inmediatas y `refresh_token` para persistencia) se gestionan e inyectan de forma encriptada en la sesión del lado del servidor.

### 4. Estado Global: TanStack Query (React Query)
Implementado en el frontend para almacenar en caché, sincronizar y actualizar el estado de los listados de eventos devueltos por el calendario de manera asíncrona, optimizando el rendimiento y evitando llamadas redundantes a la API de Google.

---

## 🚀 Despliegue en Vercel

1. Sube el repositorio a GitHub.
2. Importa el proyecto en tu dashboard de Vercel.
3. Configura las siguientes variables de entorno (`Environment Variables`) en los ajustes del proyecto de Vercel:
   * `GOOGLE_GENERATIVE_AI_API_KEY`
   * `GOOGLE_CLIENT_ID`
   * `GOOGLE_CLIENT_SECRET`
   * `NEXTAUTH_SECRET`
   * `NEXTAUTH_URL` (Tu URL final de Vercel)
4. Asegúrate de añadir la URL de producción generada por Vercel en la **Google Cloud Console** dentro de las "URIs de redirección autorizadas".This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.
