---
title: "React.js - Create-React-App!"
categories: 
  - React
tags:
  - react
  - components
  - npx
  - 
toc: true
toc_sticky: true
toc_label: "주요 목차"
---

# {{ page.title }}


## 1. Create react App
먼저, 다들 [Node](https://nodejs.org/ko)는 설치되어 있다고 가정하에 진행하겠습니다.(npm version 5.2 이상)

```
npx create-react-app react-test-app
```

## 2. Files & Folders
```json
{
  "name": "react-analysis",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.11.4",
    "@testing-library/react": "^11.1.0",
    "@testing-library/user-event": "^12.1.10",
    "react": "^17.0.1",
    "react-dom": "^17.0.1",
    "react-scripts": "4.0.2",
    "web-vitals": "^1.0.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```