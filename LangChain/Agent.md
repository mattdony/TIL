Date: 2024.06.14

## Agent란?
- 사용자의 입력(요청)을 이해하고 문제 해결을 위해 주어진 작업 도구들 중 필요한 도구와 작업 순서를 스스로 판단하고 해당 작업을 수행해 요청 사항에 대한 답변을 제공해주는 기능이다.
- LLM 기반의 "생각의 사슬 (COT / Chain of Thought)", "추론과 행동(Reasoning and Acting)에 따른 반응" 엔지니어링 기술을 활용한다.
	- References - [COT](https://arxiv.org/abs/2201.11903) / [REACT](https://arxiv.org/abs/2210.03629)
- API 등을 작업 도구로 하여 LLM이 훈련하지 못한 경험에 대해서도 정확한 답변이 가능하도록 한다.
