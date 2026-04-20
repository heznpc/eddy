# eddy — Review (2026-04-11)

## 1. 커밋 톤이 주장을 일관되게 지지하는가?

**판정: 매우 일관됨 (11 commits, 2026-03-18 → 04-04). CI/CD 인프라 갖춘 안정적 워크플로.**

```
f2a7525 fix: use git add -f for PDF ignored by .gitignore               (~2026-04-04)
23377c4 feat: add verification cost nuance, novelty decay bound, medication condition
3f83a6c chore: remove compiled PDF, add *.pdf to gitignore
dd1aaa2 chore: gitignore local files (.idea, .claude, TODO)
28da9a7 Build PDF from LaTeX source                                     (CI bot)
69fc98d Strengthen paper with new citations, experiment design, ethical framing
87468e4 Add Zenodo DOI and license badges to README
4f5fffe Build PDF from LaTeX source                                     (CI bot)
0ade30f Fix CI: add contents write permission for PDF commit
bbb721d Add GitHub Actions PDF build, remove stale local PDF
b7651a1 Initial commit: Eddy position paper v1.1                        (~2026-03-18)
```

진화 패턴:
- **t=0 (3/18)**: position paper v1.1로 시작 — *v1.0이 어디 있었는지는 미상*. 이미 8쪽 ACM SIGCONF 형식으로 외부에서 만들어진 후 import.
- **t+1 day**: GitHub Actions PDF build CI 즉시 추가. 학술 paper 레포 중 *맨 처음부터 CI*를 갖춘 드문 케이스.
- **t+2 days**: README에 Zenodo DOI(10.5281/zenodo.19074337) + CC BY 4.0 badge. 즉 *공개 가능한 학술 산출물*로서 즉시 배포 가능 형태.
- **3주 후 (3/26)**: "Strengthen paper with new citations, experiment design, ethical framing" — 5개 핵심 인용 추가(Barack 2024, Meredith 2025, Wolf 2025, Le Cunff 2024, Cortese 2025), Barkley "superpower critique" 대응 섹션 추가, METR RCT 한계 논의, 2x2 실험 설계.
- **3월 말~4월 초 (4/4)**: "verification cost nuance, novelty decay bound, medication condition" — Risko 2016 verification behavior 인용 추가, novelty decay temporal curve 구체화(plateau 1-2주 → decline 2-4주), medication을 status covariate + within-subjects washout으로 통합.

톤 일관성:
- 핵심 주장(ADHD's rapid engagement = competitive advantage in AI-augmented multi-session orchestration; remaining cognitive step after switching = re-engagement; "eddy" = 회로형 재참여 패턴)이 *모든 단계에서 단조 강화*. v1.1 이후 핵심 hypothesis는 변함 없음.
- *Self-criticism 디시플린 강함*: "superpower myth" 비판을 정식 subsection으로 흡수, *environment-specific advantage* (universal X), 임상적 지원 필요성 불변 명시, sickle cell analogy로 환경×특성 상호작용 framing. 이는 reviewer가 처음 짚을 가장 위험한 부분을 *paper 안에서 선제 대응*.
- *Falsifiability 명시*: 2x2 실험 설계 + IDE telemetry + foraging-task baseline + switching-preference screening. position paper지만 *empirical 검증 경로*가 아주 구체적.
- TODO.md(116줄)가 *commit message와 일대일 매핑*: "✓ 5 citations added", "✓ Barkley response", "✓ METR limitation"... 이는 academic paper 워크플로에서 가장 깔끔한 자기 추적.
- 약점: 4월 4일 이후 1주일 동안 0 commit. ASSETS 2026 마감(6/24)까지 시간 여유 있으나 pilot 미착수.

## 2. 부가 서비스 품질

**판정: 부가 서비스 = GitHub Actions CI/CD + Zenodo DOI. 코드 인프라는 없음.**

서비스 1: **GitHub Actions PDF build (`.github/workflows/build-pdf.yml`)**
- `xu-cheng/latex-action@v3` (Full TeX Live)
- `paper/latex/**` 변경 시 자동 트리거
- artifact 업로드 + git auto-commit + push
- *contents write permission 명시*: 4/4 commit에서 fix
- 본 survey 21개 paper 중 LaTeX CI를 갖춘 *유일한* 케이스 (canary는 vitest CI). 저자가 BasicTeX 환경 한계까지 CLAUDE.md에 문서화 (한/영 양쪽).

서비스 2: **Zenodo DOI (10.5281/zenodo.19074337)**
- 첫 commit 직후 Zenodo 업로드 + DOI 발급
- README 상단에 badge로 노출
- CC BY 4.0 라이선스로 *citation handle* 즉시 확보. arXiv endorsement를 못 받은 상태에서도 Zenodo timestamp가 우선권을 보장.

레포 구성:
- `paper/latex/main.tex` (557줄) — 단일 파일
- `paper/latex/main.pdf` — CI가 자동 생성·커밋
- `paper/latex/acmart.cls` — gitignore (CTAN에서 fetch)
- `paper/latex/main.log` — debug 산출물
- `references.bib` 없음. main.tex 내부에 \bibliography 처리 (혹은 inline). 확인 필요.

품질 평가:
- LaTeX CI는 매우 단순하지만 *학술 paper repo의 표준 best practice*. 본 survey 21개 중 다른 paper가 이 패턴을 채택하지 않은 것이 드물다.
- 데이터/코드/실험 노트북/대시보드 — 모두 0개. 순수 *theory + experimental design proposal* paper.

## 3. 고도화 가능 파트

높은 우선순위 (논증 완성):
1. **Pilot study (n=10-20)** — TODO #6. 가장 큰 게이트. 본인 + 친구 + Reddit r/ADHD에서 ADHD-C/HI/NT 5-10명씩 모집 → IDE telemetry + TTFCA + foraging task → 통계 분석. *최소한* descriptive stat이라도 제시되면 position paper → empirical paper로 한 단계 점프.
2. **E-β1 ADHD 지식 노동자 온라인 설문 (n=100-200)** — Reddit r/ADHD 모집. Pilot 전 *현장 목소리* 확보. 4-6주 작업, IRB exempt 가능. paper §3 background를 *first-hand evidence*로 강화.
3. **E-β2 Campbell et al. 2024 데이터 재분석** — 49명 ADHD knowledge worker 공개 데이터에 Wolf triadic switching, agent usage pattern, multi-session 신호를 재코딩. *기존 데이터로 즉시 가능한 secondary analysis*. 1쪽짜리 figure로 paper §2 강화.
4. **Computational psychiatry 관련 정확한 인용** — TODO #7에서 미확인. Neuropsychopharmacology 2025 ADHD computational paper의 정확한 reference 확정.

중간 우선순위:
5. **2x2 실험의 power analysis** — n=10-20로 어떤 effect size를 detect 가능한가. G*Power 시뮬레이션 1쪽 추가. reviewer가 첫 round에서 짚는 약점.
6. **Wolf triadic switching preference 사전 설문** — 실제 도구 (Qualtrics 또는 LimeSurvey)로 deploy. survey instrument 자체가 reusable.
7. **References.bib 분리** — 현재 main.tex 안에 인용 정보가 어떻게 들어가 있는지 불명. 표준 .bib 파일로 분리하면 paper portability 향상.

낮은 우선순위:
8. NIMH RFA-MH-26-195 펀딩 검토 ($3M).
9. arXiv 대시보드 통합.
10. 한국어 abstract.

> 배포/제출 관련 할 일 (arXiv endorsement, CHI Workshop proposal 등)은 논증 완성과 별개이므로 `../submissions/assets-2026/NOTES.md` 참조.

## 4. 학술적 / 시장 가치 (글로벌, 2026-04-11 기준)

### 학술적 가치: **상위권 (working paper 기준 상위 ~15%, neurodivergent HCI 한정 시 top ~10%)**

차별점:
- **Counterintuitive thesis**: ADHD = competitive advantage. 기본 disability framing의 *완전한 inversion*. 이런 inversion paper는 reviewer 관심도가 매우 높다.
- **"Eddy" naming**: 회로형 재참여 패턴의 새 이름. 인용 가능한 vocabulary anchor.
- **Convergent evidence framing**:
  - Barack 2024 (foraging, PNAS): ADHD-associated exploration → higher reward rates
  - Meredith 2025 (computational): exploratory agents > methodical in high-entropy environments
  - Grace 2001 / Badgaiyan 2015: phasic dopamine novelty response
  - Altmann & Trafton / Risko 2016: resumption lag + verification behavior
  세 개 라인을 한 hypothesis로 통합하는 cross-disciplinary synthesis.
- **Falsifiability 명시**: 2x2 design + IDE telemetry + foraging baseline + switching screen. position paper지만 *empirical 검증 경로*가 매우 구체적. ASSETS/CHI reviewer가 좋아함.
- **자기 비판의 *형식적 흡수***: Barkley superpower critique를 정식 subsection으로 처리. METR RCT(single-session)와 multi-session의 구분. Wolf triadic switching의 *전환 회피 user 한정* boundary condition. **모든 핵심 반론을 paper 안에서 선제 대응**.
- **CC BY 4.0 + Zenodo DOI**: 즉시 cite 가능한 timestamp.

위험:
- **Pilot 데이터 0건** — position paper는 이론만으로는 ASSETS 2026 main track 어렵다. workshop track은 가능하지만 main track은 50%+ 확률 reject.
- **단일 저자 (heznpc)**: clinical ADHD 영역. 정신의학/HCI 공동저자 부재. reviewer가 임상 타당성 의심.
- **Self-experimentation의 confound**: 본인이 ADHD-C/HI인지 NT인지 명시 안 됨. 본인 사례를 일반화하는 것이 *validity* 약점.
- **"Superpower myth" 인식**: paper가 이를 알고 대응하지만, *Barkley/Hinshaw/Faraone* 같은 저명 ADHD researcher가 review에 들어가면 더 강하게 짚을 가능성.
- **Novelty decay bound** — 1-2주 plateau / 2-4주 decline은 *추정*. 이를 입증하는 inter-session interval 데이터가 paper 안에 0건.

(venue-fit 분석 및 게재 전망은 `../submissions/assets-2026/NOTES.md`로 이동.)

### 시장 가치: **중상위 (특히 neurodivergent dev community + AI tool vendors에서 강함)**

- **AI coding tool 회사**: Anthropic, GitHub Copilot, Cursor, Lovable, Windsurf가 *neurodivergent-friendly mode* 광고에 즉시 사용 가능. ADHD가 *advantage*라는 framing은 마케팅 가치 매우 높음.
- **Neurodivergent dev community**: r/ADHDprogrammers, ADHD Twitter/Bluesky가 즉시 픽업할 콘텐츠. viral potential 매우 강력.
- **HR/Workplace consulting**: neurodiversity hiring 분야에서 인용 가능. Microsoft Neurodiversity Hiring Program, SAP Autism at Work 같은 기업 프로그램의 *학술적 정당화*.
- **언론**: WIRED, The Atlantic, NYT가 좋아할 톤. "ADHD는 결함이 아니라 AI 시대의 advantage" 헤드라인.
- **임상**: ADHD coach, psychiatrist에게 *환자 강점 확인* 도구. ADDitude Magazine, CHADD 자문 가능.
- 한계: position paper는 *직접* 시장 가치 변환 어려움. 후속 empirical paper가 있어야 인용 폭발 가능.

### 종합 평점 (2026-04-11)

| 축 | 점수 | 코멘트 |
|---|---|---|
| Originality of framing | 9/10 | Inversion of ADHD framing + "eddy" naming |
| Theoretical synthesis | 8/10 | foraging + computational + dopaminergic 통합 |
| Empirical contribution | 1/10 | 0개. 2x2 design만 제안 |
| Self-criticism / falsifiability | 9/10 | Barkley critique + METR limitation 선제 흡수 |
| Repo health (CI, Zenodo, badges) | 9/10 | 11 commits, GitHub Actions, DOI, CHANGELOG, CLAUDE.md |
| Submission readiness | 6/10 | LaTeX 빌드 자동, but pilot 0건 |
| Timing | 9/10 | AI agent 모멘텀 + ADHD 담론 정점 |
| Practical applicability | 7/10 | dev tool 광고에 즉시 사용 가능 |
| **Overall (position paper)** | **7.2/10** | "잘 정리된 hypothesis, 검증만 부족" |

핵심 격언: **"pilot n=10-20 + arXiv endorsement 두 가지만 추가하면 8.0+로 점프."** position paper로서는 본 survey 21개 중 *완성도 가장 높은* 케이스. 자기 비판이 paper 안에 형식적으로 흡수돼 있어 reviewer 친화적. 단일 저자라는 약점만 임상 공동저자로 보강하면 academic + market 양쪽에서 임팩트 확실.
