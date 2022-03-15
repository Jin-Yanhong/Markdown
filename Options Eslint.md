## Eslint 配置项

### package.json

```json
{
    "eslintConfig": {
        "root": true,
        "env": {
            "node": true
        },
        "extends": ["plugin:vue/essential", "eslint:recommended"],
        "parserOptions": {
            "parser": "babel-eslint"
        },
        "rules": {
            "no-debugger": "off",
            "no-console": "off",
            "no-empty": "off",
            "no-unused-vars": "off"
        }
    }
}
```

### .eslintrc.js

```javascript

```

## .eslintignore（忽略文件）
