# AWS S3 정적 웹사이트 배포 문서

## 배포 아키텍처
<img width="627" alt="AWS 배포 아키텍처" src="https://github.com/user-attachments/assets/d4ccc3ae-d31a-4140-b9c4-b12fb49b0284" />

## 목차
* [주요 링크](#주요-링크)
* [GitHub Actions와 CI/CD](#github-actions와-cicd)
* [S3와 Storage](#s3와-storage) 
* [CloudFront와 CDN](#cloudfront와-cdn)
* [캐시 무효화](#캐시-무효화)
* [Repository Secret과 환경변수](#repository-secret과-환경변수)

## 주요 링크

🔗 **웹사이트 엔드포인트**
- AWS S3 버킷: http://hanghae99-s3-4th.s3-website.ap-northeast-2.amazonaws.com
- CloudFront: https://d1bswzikqo4to6.cloudfront.net

## GitHub Actions와 CI/CD

GitHub Actions는 GitHub에서 제공하는 CI/CD 플랫폼으로, 코드의 빌드, 테스트, 배포 과정을 자동화할 수 있습니다. YAML 파일을 통해 워크플로우를 정의하여 사용합니다.

### 주요 특징
* 워크플로우 자동화
* 이벤트 기반 실행 (push, pull request 등)
* YAML 기반 설정

### CI/CD 개념

**📦 Continuous Integration (지속적 통합)**
* 여러 개발자의 코드 변경사항을 정기적으로 통합
* 자동 테스트 실행으로 버그 조기 발견
* 코드 품질 유지

**🚀 Continuous Deployment (지속적 배포)**
* 배포 과정 자동화로 인적 오류 최소화
* 코드 변경 시 자동 배포 (예: AWS S3)
* 빠른 피드백과 반복 가능한 배포 프로세스

## S3와 Storage

Amazon S3(Simple Storage Service)는 확장 가능한 객체 스토리지 서비스입니다. 정적 웹사이트 호스팅에 활용할 수 있으며, 높은 내구성과 가용성을 제공합니다.

### 주요 기능
* 정적 웹사이트 호스팅
* 버전 관리
* 접근 제어
* 데이터 암호화

## CloudFront와 CDN

CloudFront는 AWS의 CDN(Content Delivery Network) 서비스입니다. 전 세계 엣지 로케이션을 통해 콘텐츠를 캐싱하고 배포하여 웹사이트의 성능을 향상시킵니다.

### 장점
* 빠른 콘텐츠 전송
* 글로벌 배포
* HTTPS 지원
* DDoS 방어

## 캐시 무효화

CloudFront의 캐시 무효화(Invalidation)를 통해 엣지 로케이션에 저장된 콘텐츠를 갱신할 수 있습니다. 
