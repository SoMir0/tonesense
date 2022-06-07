# Tonesense

A small note taking app, transferred from my deleted repo. Under development.

## Development

```shell
git clone https://github.com/SoMir0/tonesense
cd tonesense
npm i
npm run dev
```

## Compile/Pack

```shell
# Build without packaging.
npm run build

# Preview your application in production mode without pack.
npm run preview

# Build and pack as a runnable program or installer.
npm run pack:win
npm run pack:mac
npm run pack:linux

# Pack for all platforms
npm run pack # Exclude mac platform, applicable to linux & win
npm run pack:all
```

Clean up the build directory

```shell
npm run clean
```
