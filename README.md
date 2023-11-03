# Next.js BankVault Integration<!-- omit in toc -->

This project documents the integration of the BankVault API with a Next.js application.

## Table of Contents<!-- omit in toc -->

- [Notes](#notes)
- [Integration Options](#integration-options)
  - [`create-next-app` Template Starter](#create-next-app-template-starter)
  - [Existing Next.js Application Integration](#existing-nextjs-application-integration)

## Notes

- The integration should provide the user with a streamlined API key creation process.
- The integration should support the App Router and Page Router Next.js routing methods.
- The integration should support both client-side and server-side rendering.
- A possible improvement could be to provide a QR Code generator component with the library that would be ready to use with the BankVault API rather than requiring the application to implement this itself.
- The `session`, `secret`, and `token` values should be managed by the BankVault API versus the application itself to simplify the process.

## Integration Options

### `create-next-app` Template Starter

- Provide a `create-next-app` template which bootstraps an example Next.js application with BankVault integration.

  ```shell
  npx create-next-app --example https://github.com/bank-vault/nextjs-starter
  ```

### Existing Next.js Application Integration

- To begin, npm packages should be created which can be used to integrate BankVault into a Next.js application.

  - Core package

    ```shell
    npm install @bank-vault/next
    ```

  - Ready to use UI components

    ```shell
    npm install @bank-vault/next-ui
    ```

- Ideally the integration would provide a `BankVaultProvider` component which can be used to wrap and provide the application with the BankVault API. The `BankVaultProvider` component would be responsible for initializing the BankVault API (including setting up the currently required scripts inline or adding them to the package directly) and hooking into the existing authentication system.

  - Preferably this wrapping would be done in a way that is agnostic to the authentication system used by the application and would not require any further changes to the application code.
    - Alternatively, perhaps popular authentication providers could be supported directly with adapter components/hooks
  - One way this could be implemented is by requiring the addition of element IDs to the underlying authentication input elements for example.
    - Currently the BankVault API requires specific `autoFocus` and `readOnly` props to be set on the authentication input elements. Ideally this would be handled by the `BankVaultProvider` component.

- For another solution, the package could provide custom React hooks that could be used to replace values for the authentication input elements with the BankVault API values directly or otherwise wrap and attach to authentication form elements.
- Potentially, custom UI components (i.e. `LoginPage`, `AuthForm`, `BankVaultInput`) could be provided and allow for prop forwarding/overriding to the underlying authentication input elements.
