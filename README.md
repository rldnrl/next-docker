# Next.js + Docker
## Branch
- Development - docker-developmenet
- Production - docker-production

## 두 환경 동일하게 Docker Compose를 이용해서 빌드함.

```
$ docker-compose build
```

## Production에서 마주쳤던 문제점
### Docker Compose로 실행을 시킬 경우 `.next`를 못 찾는 문제가 발생
```
$ docker-compose up
```

```
next-docker-web-1  | ready - started server on 0.0.0.0:3000, url: http://localhost:3000
next-docker-web-1  | info  - SWC minify release candidate enabled. https://nextjs.link/swcmin
next-docker-web-1  | Error: Could not find a production build in the '/app/.next' directory. Try building your app with 'next build' before starting the production server. https://nextjs.org/docs/messages/production-start-no-build-id
next-docker-web-1  |     at NextNodeServer.getBuildId (/app/node_modules/next/dist/server/next-server.js:116:23)
next-docker-web-1  |     at new Server (/app/node_modules/next/dist/server/base-server.js:70:29)
next-docker-web-1  |     at new NextNodeServer (/app/node_modules/next/dist/server/next-server.js:63:9)
next-docker-web-1  |     at NextServer.createServer (/app/node_modules/next/dist/server/next.js:140:16)
next-docker-web-1  |     at async /app/node_modules/next/dist/server/next.js:149:31
next-docker-web-1  | error Command failed with exit code 1.
next-docker-web-1  | info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
next-docker-web-1 exited with code 1
```

## 그러나 Docker로 실행할 때는 된다.

```
$ docker run -p 3000:3000 next-docker-web
```

# 결론
- 개발 환경에서는 `docker-compose`를 이용해서 개발 서버로 활용한다.
- stage나 production 환경에서는 `docker` 명령어를 활용한다.