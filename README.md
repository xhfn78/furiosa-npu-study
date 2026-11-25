# furiosa-npu-study

FuriosaAI NPU 위에서 `furiosa-llm`으로 LLM(Qwen3-8B-FP8)을 서빙하고, OpenAI 호환 API와 LangChain으로 호출해 본 실습 코드입니다.

## 서버 실행 (NPU 장비)

```bash
furiosa-llm serve furiosa-ai/Qwen3-8B-FP8 \
    --devices npu:7 \
    --host 0.0.0.0 \
    --port 8000 \
    --enable-overlap-scheduling \
    --tool-call-parser hermes \
    --enable-auto-tool-choice
```

클라이언트 코드는 `http://127.0.0.1:8000/v1` 에 접속합니다 (`api_key='EMPTY'`).

## 구성

| 폴더 | 내용 |
|---|---|
| `furiosa1/` | 기본 호출, 튜토리얼, tool calling, LangChain 연동, TPS 측정, 스트리밍, 공통 모듈(`a_kingkeras.py`) |
| `furiosa2/` | latency / TTFT / prefill·decode / 토큰 사용량, continuous batching, KV cache·prefix cache, 동시 요청·RPS, 서버 메트릭, tool calling, LangChain agent |

`furiosa2/kingkeras.py` 에 공통 함수(`get_llm`, `run_once`, `get_cache_metrics`)가 있습니다.

## 환경

```bash
pip install openai langchain langchain-openai
```
