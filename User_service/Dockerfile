# Python 3.9 경량화 이미지를 기반으로 실행
FROM python:3.9-slim

#작업 디렉토리 설정
WORKDIR /app

#필요한 시스템 패키지 설치
## default-libmysqlclient-dev는 mysqlclient를 빌드하기위함
RUN apt-get update && apt-get install -y \
    default-libmysqlclient-dev \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

RUN pip install gunicorn
#pip 업그레이드 
RUN python -m pip install --upgrade pip

#필요 패키지 설치
COPY requirements.txt .
RUN pip install -r requirements.txt

# 소스코드복사
COPY . .

# 컨테이너 실행 시 Django 서버를 Gunicorn으로 실행
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "User_service.wsgi:application"]