# tongsasa-play

전북대 eNook 강의자료 **《통계적 사고와 사회》**(한경수)용 **브라우저 실행 R/Python 실습 환경**입니다.
[JupyterLite](https://jupyterlite.readthedocs.io/) 기반 — **서버·설치 없이** 정적 GitHub Pages에서 그대로 동작합니다(WebAssembly).

## 무엇을 할 수 있나
- **Python (Pyodide)** · **R (webR)** 커널을 브라우저에서 바로 실행
- 교재 데이터(CSV) **전량 사전 탑재** → `data/` 폴더에서 바로 `read.csv` / `pd.read_csv`
- `ipywidgets` 인터랙티브 위젯(슬라이더→그래프) 지원 — 표집분포·부트스트랩 등 시연

## 접속
- 전체 실습환경(Lab): `https://guebin.github.io/SS2026-Play/lab/index.html`
- 단일 셀(REPL, iframe 임베드용): `.../repl/index.html?kernel=python`

## Quarto 책에 임베드 (예)
```html
<iframe src="https://guebin.github.io/SS2026-Play/repl/index.html?kernel=python&toolbar=1"
        width="100%" height="500" loading="lazy"></iframe>
```

## 구조
| 경로 | 설명 |
|---|---|
| `content/` | 번들될 노트북 + `content/data/` CSV (브라우저 파일시스템에 마운트) |
| `requirements.txt` | JupyterLite 빌드 도구 + 커널(pyodide·webR) + ipywidgets |
| `jupyter_lite_config.json` | 빌드 설정(번들 콘텐츠·앱) |
| `.github/workflows/deploy.yml` | 빌드 → GitHub Pages 자동 배포 |

## 로컬 빌드
```bash
uv venv .venv && source .venv/bin/activate
uv pip install -r requirements.txt
jupyter lite build --output-dir _output
python -m http.server 8000 -d _output   # http://localhost:8000/lab
```

> webR(R 커널)은 r-wasm/jupyterlite-webr-kernel(git) 사용. 빌드 시 Node 20 필요(labextension).
