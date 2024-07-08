# Next.js Firebase Form Template

![CI](https://github.com/Dyltom/nextjs-firebase-form-template/workflows/CI/badge.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

This project is a form template built with Next.js, integrating Firebase for data storage and shadcn/ui for the user interface components. It provides a customizable starting point for creating web forms that submit data to Firebase Firestore.

## Features

- Next.js framework for server-side rendering and routing
- Firebase Firestore integration for data storage
- Form validation using Zod and React Hook Form
- UI components from shadcn/ui
- TypeScript support
- Secure Firestore rules for production use

## Prerequisites

Before you begin, ensure you have the following installed:

- Node.js (v21 or later)
- npm or yarn
- A Firebase account and project

## Getting Started

1. Click the "Use this template" button on GitHub to create a new repository from this template.

2. Clone your new repository:

   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

3. Install dependencies:

   ```bash
   npm install
   # or
   yarn install
   ```

4. Set up your Firebase configuration:

   - Create a new Firebase project in the [Firebase Console](https://console.firebase.google.com/)
   - Add a web app to your project and copy the configuration
   - Create a `.env.local` file in the root directory and add your Firebase config:

     ```
     NEXT_PUBLIC_FIREBASE_API_KEY=your_api_key
     NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_auth_domain
     NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project_id
     NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_storage_bucket
     NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_messaging_sender_id
     NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id
     NEXT_PUBLIC_FIREBASE_MEASUREMENT_ID=your_measurement_id
     ```

5. Update Firebase initialization:

   Ensure your `lib/firebase.ts` file correctly initializes Firebase:

   ```typescript
   import { initializeApp } from "firebase/app";
   import { getFirestore } from "firebase/firestore";

   const firebaseConfig = {
     apiKey: process.env.NEXT_PUBLIC_FIREBASE_API_KEY,
     authDomain: process.env.NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN,
     projectId: process.env.NEXT_PUBLIC_FIREBASE_PROJECT_ID,
     storageBucket: process.env.NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET,
     messagingSenderId: process.env.NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID,
     appId: process.env.NEXT_PUBLIC_FIREBASE_APP_ID,
     measurementId: process.env.NEXT_PUBLIC_FIREBASE_MEASUREMENT_ID,
   };

   const app = initializeApp(firebaseConfig);
   export const db = getFirestore(app);
   ```

6. Set up Firestore:

   - In the Firebase Console, create a Firestore database
   - Start in test mode for development purposes

7. Run the development server:

   ```bash
   npm run dev
   # or
   yarn dev
   ```

8. Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## Firestore Security Rules

For development, you can use the following permissive rules:

```javascript
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

For production, implement more restrictive rules. Here's a basic example:

```javascript
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false;
    }

    match /users/{userId} {
      allow read, create, update: if request.auth != null && request.auth.uid == userId;
      allow delete: if false;
    }
  }
}
```

Adjust these rules based on your specific security requirements.

## Customization

- Modify the `UserForm` component in `components/UserForm.tsx` to add or remove form fields
- Update the Zod schema in `components/UserForm.tsx` to change validation rules
- Customize the UI by modifying the shadcn/ui components or adding your own styles

## Deployment

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out the [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.

## Troubleshooting

If you encounter issues with Firestore connections:

1. Ensure all environment variables are correctly set
2. Verify your Firebase project settings, especially the project ID
3. Check for any CORS issues if running locally
4. Clear browser cache and cookies
5. Test in different browsers
6. Use the Firebase Emulator Suite for local testing

## Learn More

To learn more about the technologies used in this project, check out the following resources:

- [Next.js Documentation](https://nextjs.org/docs)
- [Firebase Documentation](https://firebase.google.com/docs)
- [shadcn/ui Documentation](https://ui.shadcn.com/)
- [React Hook Form Documentation](https://react-hook-form.com/)
- [Zod Documentation](https://zod.dev/)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
