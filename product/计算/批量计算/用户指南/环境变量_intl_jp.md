## 概要情報

Batchは、タスクによって使用されるインスタンスでタスク関連の環境変数情報を提供します。これは、ユーザープログラムが環境変数に従って異なる計算タスクを実行するのに便利です。

## 詳細情報

| 変数名 | 変数の日本語名 | 変数の意味 |
|---------|---------|---------|
| BATCH_JOB_ID | ジョブ ID | インスタンスが属するジョブのID。ジョブを提出した後の戻り構造に含まれています。例えば、job-n4ohivif |
| BATCH_TASK_NAME | タスク名 | インスタンスが属するタスクの名前。ジョブを提出する時に指定されます。例えば、`"TaskName": "Task1"` |
| BATCH_TASK_INSTANCE_NUM | タスクインスタンスの総数 | インスタンスが属するタスクの同時リクエストインスタンス総数。例えば、`"TaskInstanceNum": 5` |
| BATCH_TASK_INSTANCE_INDEX | タスクインスタンス番号 | インスタンスが所属するタスク内のインスタンス番号。例えば、タスクで5つのインスタンスを同時に実行するように指定されている場合、5つのインスタンスのシリアル番号は0 1 2 3 4です |



