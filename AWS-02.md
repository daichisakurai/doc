# Amazon Auroraにおける⾼可⽤性の実現①

## Amazon Aurora
商⽤データベースの1/10のコストでMySQL とPostgreSQLと互換性があり、⾼いパフォーマンスと可⽤性を実現するために設計

https://aws.amazon.com/jp/rds/aurora/

## データベースの障害の種類

|  種類  |  説明  |
| ---- | ---- |
|  ディスク障害  |  複数のディスクで冗⻑化されている環境で、1本のディスクが物理的に完全に壊れた状況  |
|  DBサーバー障害  |  CPU故障などで、1台のコンピュータが物理的に完全に壊れた状況  |
|  データセンター障害  |  電⼒、空調、ネットワーク障害などで、データセンター規模で障害が発⽣した場合。AWSの場合、AZ障害を想定  |
|  データ破損  |  ユーザーエラーにより論理的にデータ破損した状況  |

---

## ディスク障害時

ディスク障害が発⽣した場合においても、Auroraストレージの冗⻑化により継続稼働可能

(2つの破損までは稼働可能3つの破損が発⽣した場合は読み込みのみ可能)

https://docs.aws.amazon.com/ja_jp/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.StorageReliability.html

https://aws.amazon.com/jp/blogs/news/amazon-aurora-under-the-hood-quorum-and-correlated-failure/

## DBサーバー障害時

マルチAZ構成を使⽤した⾼可⽤性構成により、1分未満でDB処理再開可能。

## データセンター障害

マルチAZ構成を使⽤した⾼可⽤性構成により、1分未満でDB処理再開可能。

シングルAZ構成の場合、同⼀AZにインスタンスの再作成を試みるが、AZそのものが障害になっている場合には、別AZにバックアップからリストア・リカバリが必要。

## データ破損時
ユーザーエラーなどによりデータが論理的に破損した場合は、バックアップからのリストア・リカバリにより対応可能だが、システム停⽌が必要Auroraバックトラックを⽤いると、より短い時間で最⼤72時間内の地点に復旧可能

---

## マルチAZ構成

https://aws.amazon.com/jp/rds/features/multi-az/