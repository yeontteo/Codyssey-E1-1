# 베이스: 공식 nginx 이미지의 alpine 버전
FROM nginx:alpine

# 이미지 설명 정보
LABEL org.opencontainers.image.title="e1-1-web" \
      org.opencontainers.image.description="Codyssey E1-1 custom nginx image"

# 실행 환경 값. docker run -e APP_ENV=... 로 바꿀 수 있다
ENV APP_ENV=dev

# nginx 이미지는 시작할 때 templates 폴더의 환경 변수를 치환해 conf.d에 설정을 만든다
COPY nginx/default.conf.template /etc/nginx/templates/default.conf.template

# 기본 환영 페이지를 직접 만든 정적 페이지로 교체한다
COPY site/ /usr/share/nginx/html/

# 프로세스가 아니라 실제 HTTP 응답으로 상태를 판단한다
HEALTHCHECK --interval=5s --timeout=3s --start-period=3s --retries=3 \
  CMD wget -q -O /dev/null http://127.0.0.1/healthz || exit 1
