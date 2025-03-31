# 꿀트립 (KKULTRIP)

## 프로젝트 소개
**"여행 명소 도슨트와 꿀팁을 제공하는 웹앱 서비스"**  
사용자의 위치를 기반으로 주변 명소를 추천하고, 명소에 대한 **정보, 스토리, 역사**를 제공하는 **도슨트 기능**과  
사용자들이 남긴 **꿀팁(명소 리뷰) 및 팁 공유 기능**을 제공하는 서비스입니다.  

<a href="https://kkultrip.newlecture.com" target="_blank">꿀트립 서비스 이동</a>

<a href="https://www.youtube.com/watch?v=2fbqxur7FEs&feature=youtu.be" target="_blank" target="_blank">시연 영상</a>




## 📅 개발 기간
- 2025년 02월 ~ 2025년 03월


## 👥 팀원
| 이름 | 역할 | Github |
|------|------|------------|
| 김재연 | 어드민페이지 |[GitHub](https://github.com/getsoss) |
| 김종윤 | 명소상세조회 |[GitHub](https://github.com/whddbsl) |
| 박소정 | 로그인, 유저페이지 |[GitHub](https://github.com/sojeong32) |
| 심동섭 | 명소 조회/검색, 꿀팁 등록/수정 |[GitHub](https://github.com/ShimDongseup) |


## ⚒️ 기술 스택
### **Frontend**
- **React**, **Next.js**, **TypeScript**, **Zustand**
- **SCSS Module**

### **Backend**
- **Node.js (Next.js API Routes)**, **Prisma ORM**
- **PostgreSQL (데이터베이스)**

### **Deployment & DevOps**
- **Nginx** (프록시 서버, 정적 파일 서빙)
- **PM2** (애플리케이션 자동 실행 및 관리)
- **GitHub Actions** (CI/CD 자동 배포)
- **Certbot** (SSL 인증서 발급, HTTPS 보안)


## ❗️ 주요 기능

1. 명소 조회, 검색필터, 지도표시
<img src="https://github.com/user-attachments/assets/8c09ad4c-32f0-4cbb-bdad-7b0efe99ee42" width="300" alt="명소조회"/>

2. 명소 상세검색 (명소정보, 도슨트, 꿀팁, 사진)

3. 꿀팁 등록/수정
<img src="https://github.com/user-attachments/assets/e4ede0d6-3749-4d8e-8637-eaf27d25cfc7" width="300" alt="꿀팁등록수정"/>

4. 유저 조회 (마이페이지, 다른유저가 올린 꿀팁조회)
<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/1ae1bb10-c55b-49c8-bd17-026fe51cc64b" width="100%" alt="마이페이지"/></td>
    <td width="100"></td>
    <td><img src="https://github.com/user-attachments/assets/aa7dd7ba-258b-4bc6-9a4c-5abaa340c9fb" width="300" alt="다른유저꿀팁조회페이지"/></td>
  </tr>
</table>

5. 어드민 페이지 (명소,꿀팁,유저 등록/조회/삭제)
<img width="1051" alt="관리자 명소조회" src="https://github.com/user-attachments/assets/cee0f41e-6c6e-4810-af7f-4562b576593a" />
<img width="1053" alt="관리자 꿀팁조회" src="https://github.com/user-attachments/assets/56a4b09b-8200-4e6f-b6d1-83df398af4f8" />
<img width="1048" alt="관리자 이미지관리" src="https://github.com/user-attachments/assets/fb85d166-0e60-4024-94e0-e95aad9c626a" />
<img src="https://github.com/user-attachments/assets/411e3f37-46c5-481e-a830-a462c3f7656b" width="300" alt="명소 수정"/>

## 📌 맡은 기능

### **1. 위치 기반 명소 검색 & 네이버 지도 연동**
- 네이버 지도 API를 활용하여 **사용자 위치를 기준으로 명소를 검색**하고 지도에 마커 표시
- 위도/경도를 기반으로 반경 2.2km 내 명소를 필터링하여 조회
- `Query Parameter` 기반 검색·필터링 기능 적용하여 **SSR(서버사이드 렌더링)로 SEO 최적화**
- 필터 적용 시 URL을 동적으로 업데이트하여 **새로고침 후에도 상태 유지**

### **2. 명소 검색 API 구현**
- 사용자가 **명소 이름 또는 지역명으로 검색**할 경우, **명소 DB 검색 + 네이버 Geocode API 활용**
- 검색 결과가 없을 경우, 네이버 Geocode API로 위도/경도를 변환하여 근처 명소를 추가 검색
- **중복된 검색 결과 제거** (명소 ID 기준)

### **3. 꿀팁(명소 리뷰) 등록 및 수정**
- 사용자가 직접 명소에 대한 꿀팁(후기)을 등록할 수 있도록 기능 구현
- 기존 꿀팁을 수정할 경우 **이전 이미지 유지** 또는 **새로운 이미지 추가 가능**
- **로컬 서버 환경에서 이미지 저장 및 관리** (파일은 `~/upload/images/tips/` 경로에 저장, DB에는 파일 경로만 저장)
- **Nginx에서 정적 파일 서빙**을 위한 `alias` 설정 적용

### **4. 평균 가격 및 대기 시간 자동 업데이트**
- 꿀팁 등록/수정 시 **명소의 평균 가격 및 평균 대기 시간 자동 업데이트**
- 기존 평균값을 고려하여 새로운 평균값을 재계산하여 반영

### **5. 서버 배포 & CI/CD 구축**
- **Nginx**를 활용하여 3000번대 포트에서 실행되는 Next.js 앱을 80번 포트로 프록시 설정
- **Certbot SSL 인증 적용**하여 HTTPS 서비스 제공 (`https://kkultrip.newlecture.com`)
- **PM2를 활용하여 애플리케이션 자동 실행 및 재시작**
- **GitHub Actions을 활용한 CI/CD 구축**
  - `develop` 브랜치에 코드 푸시 시, 자동으로 배포 스크립트 실행
  - `pm2 restart 0`을 통해 서버 자동 재시작


## 성과 및 배운 점
* SSR 및 CSR을 적절히 활용하여 SEO 최적화
* 쿼리 기반 필터링 및 정렬 기능으로 사용자 경험(UX) 개선
* 클린 아키텍처 적용하여 유지보수성과 확장성 향상
* CI/CD 구축을 통한 배포 자동화로 운영 효율성 향상  
