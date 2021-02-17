# Celery Structure

celery 구조입니다. django 프로젝트 구조를 보고 작성했고 `settings.py`에서 각각의 태스크를 모듈로 등록하는 방식을 채택했습니다.

## settings.py
[Configuration and default - Celery Docs](https://docs.celeryproject.org/en/stable/userguide/configuration.html#new-lowercase-settings) 참고하여 추가로 설정을 등록할 수 있습니다. 아래 세팅은 브로커로 Redis를 사용할 때에 간단한 설정 방법입니다.

`imports`에서 `apps` 폴더에 작성한 shared_task 를 등록하는 방식입니다.

```python
# Settings Timezone
timezone = "Asia/Seoul"

# Settings Broker URL
broker_url = "redis://localhost:6379/0"

# Settings Result Backend URL
result_backend = "redis://localhost:6379/0"

# Settings task imports
imports = [
    "mytask.apps.sample",
]
```

## Task Example
Task는 가장 많이 사용되는 함수형 방식을 채택했고, `shared_task`를 이용해서 imports 설정을 이용할 수 있도록 작성했습니다.

```python
from celery import shared_task

@shared_task(name="plus")
def plus(x: int, y: int) -> int:
    return x + y
```
