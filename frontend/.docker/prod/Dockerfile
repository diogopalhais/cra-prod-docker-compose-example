FROM node:11-alpine as builder

ARG REACT_APP_API_URL
ENV REACT_APP_API_URL=${REACT_APP_API_URL}

WORKDIR /usr/src/frontend
COPY . .

RUN yarn install --frozen-lockfile --no-cache --production
RUN yarn run build 

# Stage 2 - the production environment
FROM nginx:alpine

COPY .docker/prod/nginx.conf /etc/nginx/conf.d/default.conf
RUN rm -rf /usr/share/nginx/html/*
COPY --from=builder /usr/src/frontend/build /usr/share/nginx/html

CMD ["nginx", "-g", "daemon off;"]


