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

GitHub에서 제공하는 자동화된 워크플로우 도구입니다. 코드가 리포지토리에 푸시되면 자동으로 빌드, 테스트, 배포 등의 작업을 수행할 수 있습니다. workflow 파일(.github/workflows/*.yml)을 통해 설정하며, 테스트 실행, 코드 품질 검사, 패키지 배포 등 다양한 CI/CD 작업을 자동화할 수 있습니다.

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

Amazon S3(Simple Storage Service)는 AWS에서 제공하는 클라우드 스토리지 서비스입니다. 정적 웹사이트 호스팅, 데이터 백업, 미디어 파일 저장 등에 사용됩니다. 버킷이라는 컨테이너에 객체(파일)를 저장하며, 높은 내구성과 가용성을 제공합니다.

### 주요 기능
* 정적 웹사이트 호스팅
* 버전 관리
* 접근 제어
* 데이터 암호화

## CloudFront와 CDN

Amazon CloudFront는 AWS의 CDN(Content Delivery Network) 서비스입니다. 전 세계에 분산된 엣지 로케이션을 통해 콘텐츠를 캐싱하고 사용자에게 가장 가까운 위치에서 콘텐츠를 제공함으로써 지연 시간을 줄이고 성능을 향상시킵니다.

### 장점
* 빠른 콘텐츠 전송
* 글로벌 배포
* HTTPS 지원
* DDoS 방어

## 캐시 무효화

CloudFront에 캐시된 콘텐츠를 강제로 업데이트하는 프로세스입니다. 원본 콘텐츠가 변경되었을 때 캐시된 이전 버전을 제거하고 새로운 콘텐츠로 업데이트하기 위해 사용됩니다. 특정 파일 경로나 와일드카드 패턴을 지정하여 무효화할 수 있습니다.

## Repository secret과 환경변수

GitHub 리포지토리에서 민감한 정보(API 키, 액세스 토큰 등)를 안전하게 저장하고 사용하기 위한 기능입니다. 리포지토리의 Settings에서 설정할 수 있으며, GitHub Actions 워크플로우에서 환경변수로 사용할 수 있습니다. 암호화되어 저장되며 권한이 있는 사용자만 접근할 수 있습니다.
