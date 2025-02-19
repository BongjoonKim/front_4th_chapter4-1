# AWS S3 정적 웹사이트 배포 문서

## 배포 아키텍처
<img width="608" alt="image" src="https://github.com/user-attachments/assets/0765362f-68e1-4c61-9f08-e013dace9594" />

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

# 성능 비교 평가

## AWS S3와 CF(CloudFront)로 배포한 경우 데이터/파일의 크기와 로딩 시간 비교

| 파일명 | S3 크기 | CF 크기 | S3 시간 | CF 시간 | 크기 차이(S3 - CF) | 시간 개선(S3 - CF) |
|--------|---------|----------|----------|-----------|------------|------------|
| 도메인 | 11.9 kB | 3.1 kB | 76 ms | 41 ms | ▼ 8.8 kB | ▼ 35 ms |
| next.svg | 1.7 kB | 1.0 kB | 66 ms | 8 ms | ▼ 0.7 kB | ▼ 58 ms |
| 05e4ebe658c1b3a7.css | 10.1 kB | 3.1 kB | 151 ms | 8 ms | ▼ 7 kB | ▼ 143 ms |
| webpack-c2bf96b4836901a1.js | 3.8 kB | 2.0 kB | 92 ms | 10 ms | ▼ 1.8 kB | ▼ 82 ms |
| 4bd1b696-20882bf820444624.js | 167 kB | 50.2 kB | 144 ms | 9 ms | ▼ 116.8 kB | ▼ 135 ms |
| 517-e7da863add2bbf63.js | 201 kB | 47.4 kB | 175 ms | 12 ms | ▼ 153.6 kB | ▼ 163 ms |
| main-app-e84e6ff14842765c.js | 828 B | 797 B | 64 ms | 11 ms | ▼ 31 B | ▼ 53 ms |
| 970-08a075b64c49a780.js | 14.6 kB | 5.6 kB | 47 ms | 11 ms | ▼ 9 kB | ▼ 36 ms |
| page-d21f7260b43e2b31.js | 564 B | 531 B | 23 ms | 11 ms | ▼ 33 B | ▼ 12 ms |
| vercel.svg | 486 B | 458 B | 13 ms | 6 ms | ▼ 28 B | ▼ 7 ms |
| file.svg | 749 B | 720 B | 57 ms | 7 ms | ▼ 29 B | ▼ 50 ms |
| window.svg | 743 B | 713 B | 175 ms | 7 ms | ▼ 30 B | ▼ 168 ms |
| globe.svg | 1.4 kB | 860 B | 63 ms | 8 ms | ▼ 540 B | ▼ 55 ms |
| 93f479601ee12b01-s.p.woff2 | 31.8 kB | 31.7 kB | 64 ms | 7 ms | ▼ 100 B | ▼ 57 ms |
| 569ce4b8f30dc480-s.p.woff2 | 28.9 kB | 28.8 kB | 129 ms | 7 ms | ▼ 100 B | ▼ 122 ms |
| favicon.ico | 26.3 kB | 26.3 kB | 41 ms | 5 ms | = 0 B | ▼ 36 ms |

개선사항:
1. 거의 모든 파일의 로딩 시간이 크게 개선되었습니다 (평균 약 76% 감소)
2. 대부분의 파일 크기가 최적화되었습니다
3. 특히 큰 JavaScript 파일들(4bd1b696, 517)의 크기가 70% 이상 감소했습니다
4. 폰트 파일과 이미지는 크기 변화가 미미하지만 나머지 파일에 대한 로딩 시간은 CloudFront에서 크게 개선되었습니다
5. 전체 페이지 로딩 시간을 비교했을 떄
      
      | 이벤트 | S3 | CloudFront | 시간 개선 | 개선율 |
      |---------|-----|------------|------------|---------|
      | DOMContentLoaded | 249 ms | 75 ms | ▼ 174 ms | ▼ 69.9% |
      | Load | 378 ms | 101 ms | ▼ 277 ms | ▼ 73.3% |
      
      페이지 로딩 성능이 크게 개선되었습니다:
      - DOMContentLoaded: 약 70% 감소
      - Load: 약 73% 감소
    
      CloudFront CDN 적용으로 전반적인 페이지 로딩 속도가 3-4배 빨라졌습니다.

## 성능 평가 결론

단순한 페이지에서도 실제 로딩 성능이 약 60 - 70% 성능 향상이 있는 것을 고려하였을 떄, 더 복잡한 웹 페이지를 CloudFront를 활용하여 배포하게 된다면 더 극적인 성능 향상을 보여줄 것으로 생각됩니다.
