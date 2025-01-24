# 1. init project

`pnpm init`

# 2. add pnpm-workspace.yaml and copy the following code into it

```
packages:
  - 'packages/*'
```

# 3. [typescript](https://www.typescriptlang.org/)

## install

`pnpm add typescript@4.7.4 -D -w`

## check the version

`pnpm tsc -v`

## init config

- [tsc CLI Options](https://www.typescriptlang.org/docs/handbook/compiler-options.html)
- [tsconfig](https://www.typescriptlang.org/tsconfig/)

`pnpm tsc -init`

# 4. [prettier](https://www.prettier.cn/)

## install the extension `Prettier - Code formatter` for vscode

## add the file .prettierrc

```
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "printWidth": 80,
  "trailingComma": "none",
  "arrowParens": "avoid"
}
```

# 5. [rollup](https://cn.rollupjs.org/introduction/)

## install rollup(at least the version 2.68.0)

`pnpm add -D -w rollup@2.68.0`

## add the file rollup.config.js

```
import resolve from '@rollup/plugin-node-resolve';
import commonjs from '@rollup/plugin-commonjs';
import typescript from '@rollup/plugin-typescript';

/**
 * 默认导出一个数组，数组的每一个对象都是一个单独的导出文件配置，详细可查：https://www.rollupjs.com/guide/big-list-of-options
 */
export default [
  {
    // 入口文件
    input: 'packages/vue/src/index.ts',
    // 打包出口
    output: [
      // 导出 iife 模式的包
      {
        // 开启 SourceMap
        sourcemap: true,
        // 导出的文件地址
        file: './packages/vue/dist/vue.js',
        // 生成的包格式：一个自动执行的功能，适合作为<script>标签
        format: 'iife',
        // 变量名
        name: 'Vue'
      }
    ],
    // 插件
    plugins: [
      // ts 支持
      typescript({ sourceMap: true }),
      // 模块导入的路径补全
      resolve(),
      // 将 CommonJS 模块转换为 ES2015
      commonjs()
    ]
  }
];
```

## add plugins

`yarn add -D -w @rollup/plugin-commonjs@22.0.1 @rollup/plugin-node-resolve@13.3.0 @rollup/plugin-typescript@8.3.4 rollup-plugin-sourcemaps@0.6.3 tslib@2.8.1`

# 6. Configure Path Mapping in the `tsconfig.json`:

```json
"compilerOptions": {
  ...
  "baseUrl": ".",
  "paths": {
    "@vue/*": ["packages/*/src"]
  }
  ...
}
```

This configuration allows you to use the `@vue/*` alias to reference files within the `packages` directory.

# 7. Add the command build in the `package.json`:

```bash
"build": "rollup -c",
```

# 8. Add the file `.gitignore`

```
dist
.DS_Store
node_modules
coverage
temp
explorations
TODOs.md
*.log
.idea
.eslintcache
dts-build/packages
*.tsbuildinfo
*.tgz
```

# 9. Push the local new project to the remote gihub repository

First create a new repository in the github, then the github will give the url `git@github.com:your-username/your-repo.git`.

```
git init

git add .

git commit -m "init"

git branch -M main

# replace the url to the new created repository in the github
git remote add origin git@github.com:your-username/your-repo.git

git push -u origin master
```
