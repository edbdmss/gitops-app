# 1. 빌드 스테이지: Eclipse Temurin JDK 17 기반의 메이븐 환경 사용
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app

# 라이브러리 캐싱
COPY pom.xml .
RUN mvn dependency:go-offline -B

# 소스 복사 및 패키징
COPY src ./src
RUN mvn clean package -DskipTests

# 2. 실행 스테이지
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# 빌드 스테이지에서 생성된 최종 jar 파일만 복사
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]