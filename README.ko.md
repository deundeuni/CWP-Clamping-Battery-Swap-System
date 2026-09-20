
> **다국어 공개 안내:** 본 문서는 동일 내용의 한/영 이중 공개 문서입니다. v2.2 2026-09-13 (영문: [README_EN.md](README_EN.md))  
> **Original Authority Notice:** 본 기술 명세의 법적·공학적 판단 최상위 기준은 한글 원본(`README.ko.md`)에 귀속되며, 영문본은 보조 참조용으로만 기능한다. (PHILOSOPHY.ko.md is authoritative original)

# CWP-Clamping-Battery-Swap-System v2.2 (CWP-ClampingLock) - 범용 중량물·소형 모듈 페일세이프 전자기 클램핑 플랫폼의 배터리 적용 실시예

* **공개 일자:** 2026-09-13 (초안 2026-08-20, v2.0 2026-08-23, v2.1 2026-09-06, v2.2 2026-09-13)
* **작성자:** deundeuni (System Architect / Natural Person Inventor)
* **라이선스:** CERN-OHL-S v2 (하드웨어/CAD/도면) | CC BY-SA 4.0 (문서/설명)
* **공개 목적:** 방어적 공개 / 선행기술(Prior Art) 등록 - 독점 특허화 방지 및 권리 침해 위험 완화
* **검색 키워드:** CWP, CWP-Clamping, CWP-ClampingLock, EPM, Electro-Permanent Magnet, 펄스 구동 영구자석, 캡티브 듀얼 핀, 3중 쿠션, 비접촉 고정, EV 배터리 스왑, 무전원 고정, Prior Art, CWP-Entry, CWP-Battery-Swap, CWP-Rolling-Self-Align, 범용 중량물 클램핑, Heavy Payload Clamping Platform, Off-Grid EPM Lock, 노지 중량 모듈 전자기 고정

---

## 0. 설계자 독자 아키텍처 및 선행기술 공개 선언 (Designer's Philosophical Declaration)

1. **설계 철학 및 공지기술의 응용적 독자성 (Architectural Conception & Prior Art Respect):**  
   본 시스템은 공지된 전자영구자석(Electro-Permanent Magnet, EPM) 펄스 극성 전환 메커니즘 및 기구학적 구속·완충 선행기술을 기초로 한다. 본 백서는 전기차, ESS, 모듈러 구조체 등 다양한 중량물 체결 시 정전이나 비상 상황에서도 무전력 자력 고정을 유지하고 안전하게 해제하고자 하는 **설계자(deundeuni)의 독자적 철학과 문제 의식**에서 출발하였다. 공지된 원리를 바탕으로 '펄스 구동 영구자석(EPM) 비접촉 체결 + 캡티브 듀얼 핀 구속 + 3중 쿠션 완충 메커니즘'을 결합하고, 범용 고정 인터페이스 파라미터를 정립한 아키텍처 결정권은 설계자 자연인에게 귀속된다. 본 시스템은 EPM 및 전자기 클램핑 기술을 개척한 선행 연구자 및 특허권자들의 공학적 성과를 존중하며, 공지 원리를 구체적 실시예 파라미터 조합으로 응용 개시함을 명시한다.

2. **소프트웨어 유틸리티 활용에 관한 명시 (Software Utility Limitation):**  
   본 문서 작성 과정에서 활용된 소프트웨어 및 AI 도구는 설계자가 이미 정의한 기술 조합, 설계 방향, 수치 파라미터를 바탕으로 단순 포맷팅, 문맥 정제, 개념 시각화 출력을 실행한 **수동적 실행 유틸리티(Passive Execution Utility)**에 국한된다. 본 인프라의 모든 설계 의도, 구조적 결합권, 선행기술 공개 권한은 전적으로 설계자 자연인에게 귀속된다.

---

## 1. 개요 및 적용 범위

### 1.1 개요
CWP-ClampingLock은 전기차, ESS, 모듈러 주택, 재난 대피소, 농기계 모듈, 물류 로봇, 드론 등 다종 중량물 및 소형 페이로드 고정을 위한 범용 EPM 마그네틱 클램핑 모듈 개념 설계이다.  
특정 기업의 독점 방식을 배제하고 상호 호환성과 무전원 유지 표준 기준을 충족하는 범용 인터페이스 구조를 지향한다.

### 1.2 적용 범위 (Application Scope)
본 구조는 EV 배터리 교환에 한정되지 않으며, 노지 및 부평탄 지형에서 중량 모듈러 주택, 재난 대피소, 농기계 모듈, 물류 파렛트 등 500kg 이상 중량물 및 소형 모듈 페이로드의 무전력 영구자석 고정, 진동 흡수 체결 및 비상 안전 해제에 범용으로 적용 가능하다. EV, ESS, 물류로봇(AGV/AMR), 드론, 선박, 항공우주, 건설·농업용 중장비 모듈 등 무전원 체결 및 클램핑이 필요한 전 분야를 포괄한다.

---

## 2. 고정 원리 및 기획 배경

* **펄스 구동 영구자석(EPM) 방식:** 순간 펄스 전원 신호로 영구자석 극성을 전환하여 체결 및 해제를 수행하며, 체결 후에는 추가 전원 공급 없이 영구자석 자체 자력으로 고정 상태를 유지하는 무전원 안전 구조를 지향함.
* **캡티브 듀얼 핀 구조:** 핀이 외부로 이탈되지 않는 내부 기계식 구속 구조를 적용하여 진동 환경에서의 이탈 방지 및 다중 체결 안정성을 도모함.
* **비접촉 자력 체결:** 자력 기반 인터페이스로 기존 접촉 기계식 구조 대비 마찰, 마모, 소음 완화를 도모함.

---

## 3. 흔들림 방지 구조 (3중 쿠션 완충 메커니즘)

* **우레탄 패드:** 배터리 및 중량 모듈 접촉면 충격 완화 및 신속 체결 완충.
* **접시 스프링:** 핀 후면 미세 진동 흡수 및 자력 인력 방향 예하중 유지.
* **에어갭 (Air Gap):** 자석과 모듈 인터페이스 사이 유연 틈새 설계를 통한 구조적 충격 분산.

---

## 3.5 CWP 3대 하드웨어 연계 및 생존 아키텍처 (CWP 3-Hardware & System Integration)

본 ClampingLock 모듈은 단독 고정 장치에 그치지 않고 CWP 3대 핵심 하드웨어 메커니즘 및 상위 생존 아키텍처와 유기적으로 결합되어 무중단 생존 지향형 교환 스테이션 및 고정밀 도킹 인프라로 동작할 수 있다.

* **진입 유도 및 1차 정렬 (`CWP-Entry`):** 세차장 V레일 및 지면 가이드 홈 인프라 원용과 라인 레이저 가이드를 통해 진입 오차를 완화하고 정비 구역으로 유도함.
* **기구적 2차 정렬 (`CWP-Rolling-Self-Align-Battery-Swap-System`):** V-홈 및 캐스터 수동/자율 정렬 메커니즘(A/B/C/S 타입)과 연동하여 진입 후 치수 오차(예: ±5mm 이상)를 물리적으로 흡수하고 정밀 도킹 구역으로 유도함.
* **차동 감속 저충격 도킹 (`CWP-Battery-Swap`):** N/(N+1) 차동 기어비(예: 60T/61T) 및 회전형 스테이지를 활용하여 도킹 상대속도를 극저속(예: 0.016rpm 수준)으로 감속시켜 완충 도킹을 지향함.
* **전자기 클램핑 및 안전 체결 (`CWP-Clamping-Battery-Swap-System` - 본 기술):** 정밀 정렬 후 EPM 마그네틱 클램핑, 이중 핀 고정 및 3중 쿠션 구조를 통해 무전력 영구자석 고정 및 비상시 안전 해제를 지향함. (배터리 팩 및 500kg 이상 범용 중량 모듈 공통 적용)
* **물리적 비상 차단·해제 (`0.1ms HW Intercept` / `LAST-LIGHT` 연계):** 화재, 정전 등 비상 상황 발생 시 Hardware Intercept 신호에 의해 EPM 클램프 자력이 역펄스 해제(Release)되거나 무전력 기계식 이탈을 지원함.
* **연산적 제어 생존 (`chiplet-apu-multi-system-survival-architecture`):** 분산 관제(CCS) 및 다중 칩렛 제어 아키텍처와 결합하여 관제 칩렛 고장 시에도 클램핑 제어 로직이 지속 동작하도록 구성함.

---

## 4. 한계, 보증 부인 및 면책 (Limitation, Disclaimer of Warranties & Liability)

본 문서는 선행기술 개시 및 방어적 공개를 목적으로 작성되었으며, 어떠한 보증도 없이 '있는 그대로(AS-IS)' 제공된다.

1. **보증 부인 (Disclaimer of Warranties):** 특정 목적 적합성, 상품성, 무결성, 제품화 가능성 및 제3자 특허 비침해를 보증하지 않는다.
2. **책임 제한 (Limitation of Liability):** 본 문서의 기술 개시 내용의 활용, 구현, 직접·간접 응용으로 인해 발생 가능한 직접 손해, 간접 손해, 징벌적 손해, 사고 또는 사업적 손실에 대해 작성자(deundeuni)는 법적 책임을 지지 아니한다.
3. **미필적 고지 및 고의 침해 배제 (Non-willful Infringement Notice):** 본 공개는 미국 특허법상 고의 침해(Willful Infringement / 35 U.S.C. §284 및 관련 판례 법리) 주장에 대한 방어적 거점을 형성하고, 공공 영역(Public Domain)에 선행기술을 명시하여 제3자의 독점적 특허 출원을 방지하기 위한 방어적 개시 조치이며, 타인의 권리를 고의로 침해하려는 의도가 없음을 명시한다.
4. **법규·안전·인증 책임:** 각 국가별 법규, 전기·소방·소음·진동 안전 기준 준수, 인증 획득 및 현장 안전 검증 책무는 전적으로 구현자 및 사업화 주체에게 귀속된다.

---

## 5. 도면 및 인공지능 시각화 면책 (Figures & AI Visualization Disclaimer)

* **주의 (AI 시각화 면책 조항):** 본 명세서의 메커니즘 개념은 작성자(deundeuni)가 독자적으로 고안했습니다. 첨부된 도면 및 개념도(예: `cwp-clampinglock-exploded-view.webp`)는 이해를 돕기 위해 범용 생성형 AI 시각화 도구를 활용하여 생성된 예시일 뿐이며, 기존 상용 제품이나 타인의 등록 특허 도면을 복제한 것이 아닙니다.
* **도면 비고:** 본 도면에 기술된 모든 치수, 유격, 수량은 예시이며 범위를 한정하지 않는다. EPM 자력 체결, 캡티브 핀 및 3중 쿠션 완충 메커니즘 구조만이 본 공개의 핵심이다.

---

## 6. 라이선스 및 상업적 이용 안내 (Licensing)

> CERN Open Hardware Licence Version 2 - Strongly Reciprocal (CERN-OHL-S v2)  
> Copyright (c) 2026 deundeuni  
>  
> This hardware design is licensed under CERN-OHL-S v2.  
> You may manufacture and distribute it, even commercially,  
> but if you distribute products based on it, you must also  
> make the modified design files available under the same license.  
>  
> Full text: https://ohwr.org/cern_ohl_s_v2.pdf  
>  
> Documentation and figures: CC BY-SA 4.0  
> https://creativecommons.org/licenses/by-sa/4.0/  

* **상업적 이용 안내:** 상업적 제조/판매 모두 가능함. CWP 부분을 개선한 도면만 같은 라이선스로 공개하면 되며, 귀사의 다른 비밀 설계까지 공개할 필요는 없음.

---

## 7. 실리보호 (Practical Protection)

* **원안 우선 원칙:** 본 명세서의 법적·기술적 해석은 한국어 원본(`README.ko.md`)을 최우선 기준으로 적용하며, 영문본 및 기타 언어 번역본은 참고용으로만 기능한다.
* **범위 포괄성:** 본 문서에 기술된 EPM 펄스 수치, 핀 지름, 쿠션 두께, 에어갭 범위 등은 광범위한 선행기술 선점을 위한 예시로서 상위개념으로 포괄 적용된다.
* **사업화 내용 분리:** 본 백서 원안에는 Pure Open Source 및 선행기술 개시 내용만을 포함하며, 독자적인 수익 모델 및 사업화 세부 실행안은 별도 기술 문서로 분리 관리한다.

---

## 8. 출처 및 기록 (Sources & Records)

* **전자기 클램핑 및 전자영구자석(EPM) 공지기술 원리 (Foundational EPM & Magnetic Clamping Prior Art)**
  * Electro-Permanent Magnet (EPM) Pulse-Switching Principles — 가역 영구자석(Alnico 등)과 비가역 영구자석(NdFeB 등)의 코일 순간 펄스 전류에 의한 극성 전환 및 무전력 자력 고정 공지 기술
  * US Patent US7999645B2 / US20100308519A1 — Electro-permanent magnetic work holding and clamping apparatus using pulse-switched reversible permanent magnets
  * US Patent US9164154B2 / EP1419034B1 — Electro-permanent magnetic clamping systems with bistable state holding and activation control
  * US Patent US10984936B2 / US8674576B2 — Electropermanent magnet arrays and actuators for robotic latching and workholding

* **기구학적 구속 및 완충 선행기술 (Kinematic Latching & Damping Prior Art)**
  * Captive Dual Pin & Mechanical Retention Mechanisms — 기계식 이탈 방지 핀 및 다중 체결 래칭 공지 구조
  * Belleville Washer (Disc Spring) & Elastomer Damping — 접시 스프링 예하중 및 우레탄 쿠션 진동 감쇄 결합 공지 기술

* **본 실시예의 공학적 차별점 (Specific Embodiment Feature)**
  * 공지된 EPM 자력 극성 전환 및 기계식 핀·스프링 완충 원리를 기초로 하되, '펄스 구동 EPM 비접촉 체결 + 캡티브 듀얼 핀 구속 + 3중 쿠션(우레탄, 접시스프링, 에어갭) 완충 메커니즘'을 범용 모듈형 인터페이스 규격 및 비상 릴리즈 제어와 결합·한정한 특정 실시예 구조에 기술적 차별성이 있음

* **소마모아 생태계 저장소 및 학술 식별자 (Ecosystem Repositories & DOIs)**
  * 상위 범용 생존 아키텍처 & APU 연산 제어기 (`chiplet-apu-multi-system-survival-architecture`) — GitHub: `deundeuni / chiplet-apu-multi-system-survival-architecture` | CERN Zenodo DOI: `10.5281/zenodo.22374987` (https://doi.org/10.5281/zenodo.22374987)
  * 재난 피난 유도 & 보조 인프라 (`LAST-LIGHT`) — GitHub: `deundeuni / LAST-LIGHT` | CERN Zenodo DOI: `10.5281/zenodo.22373189` (https://doi.org/10.5281/zenodo.22373189)
  * CWP 전자기 클램핑 (`CWP-Clamping-Battery-Swap-System`) — CERN Zenodo DOI: `10.5281/zenodo.22373722` (https://doi.org/10.5281/zenodo.22373722)
  * CWP 배터리 교환 도킹 (`CWP-Battery-Swap`) — CERN Zenodo DOI: `10.5281/zenodo.22373538` (https://doi.org/10.5281/zenodo.22373538)
  * CWP 롤링 셀프얼라인 (`CWP-Rolling-Self-Align-Battery-Swap-System`) — CERN Zenodo DOI: `10.5281/zenodo.22373704` (https://doi.org/10.5281/zenodo.22373704)
  * CWP 진입 유도 정렬 (`CWP-Entry`) — GitHub: `deundeuni / CWP-Entry`
  * 최상위 거점 관문 및 메인 저장소 (`soma-moa`) — GitHub: `deundeuni / soma-moa` | 관문 도메인: `somamoa.ai.kr`

* **법적 근거 및 선사용권·미필적 고지 규정 (Legal Statutes & Precedents)**
  * 대한민국 특허법 제103조 — 선사용에 의한 통상실시권
  * 미국 특허법 35 U.S.C. §273 — Defense to Infringement Based on Prior Commercial Use
  * 미필적 고지 및 방어적 개시 규정 — 본 문서는 미국 특허법상 고의 침해(Willful Infringement / 35 U.S.C. §284 및 관련 판례 법리) 주장에 대한 사전 방어 논리를 제공하고, 공공 영역(Public Domain)에 선행기술을 명시적으로 개시하여 제3자의 독점 특허화를 방지하기 위한 방어적 공개(Defensive Publication) 목적으로 공개되었음.
