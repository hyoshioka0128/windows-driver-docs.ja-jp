---
title: ファームウェア更新の状態
description: この時点で、すべてのファームウェアの更新プログラムが適用され、Windows OS ローダーの後続の呼び出し時に、ESRT ですべての更新プログラムの結果が反映されることが期待されます。
ms.assetid: 988B1E95-2268-4B4F-B0C6-3C965FCD1B1C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e397833e94ce9cc45c5a1d9dbefeace8945de10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337591"
---
# <a name="firmware-update-status"></a>ファームウェア更新の状態


この時点で、すべてのファームウェアの更新プログラムが適用され、Windows OS ローダーの後続の呼び出し時に、ESRT ですべての更新プログラムの結果が反映されることが期待されます。 ESRT 例を参照する[ESRT テーブル定義](esrt-table-definition.md)とのファームウェア リソース更新のドライバー パッケージ INF 例[update のドライバー パッケージの作成](authoring-an-update-driver-package.md)firmware.bin のバージョン 2 の場合、ファームウェアで正常に適用するには、し、新しい ESRT テーブルはこれを反映します。 テーブル内の唯一の違いは、システム ファームウェア リソース エントリのファームウェアのバージョンと最後の試行バージョン フィールドが正常に適用された新しいファームウェアのバージョンを反映するように変更されたことがわかります。

| フィールド                               | Value                     | Comment                                                                                                                                                                                                              |
|-------------------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ファームウェアのリソースの数             | 2                         | このテーブルには、2 つのファームウェア リソース エントリが含まれています。                                                                                                                                                                   |
| ファームウェアのリソースの最大数           | 2                         | このテーブルの割り当てには、2 つのリソースの最大値を記述するのに十分な領域が含まれています。                                                                                                                                  |
| リソースのファームウェア バージョン           | 1                         | このテーブルを使用してファームウェア リソース エントリの形式バージョンには 1 です。                                                                                                                                                     |
| ファームウェア リソース エントリの配列       | ファームウェア リソース エントリ 0 |                                                                                                                                                                                                                      |
|   ファームウェア クラス                    | (システム\_ファームウェア)        | この GUID は、システム ファームウェア PnP を使用して更新プログラムを識別します。                                                                                                                                                         |
|   ファームウェアの種類                     | 1                         | システム ファームウェアの種類には 1 です。                                                                                                                                                                                           |
|   ファームウェア バージョン                  | 2                         | 現在システム ファームウェアのバージョンには 2 です。                                                                                                                                                                            |
|   サポートされているファームウェアの最小バージョン | 2                         | 2 に、サポートされているファームウェアの最小バージョンを変更、ファームウェアは、バージョンにロールバックをより前のバージョン 2 することはできません。 この値は通常、ファームウェアの更新には、セキュリティ修正プログラムが含まれている場合に変更します。 |
|   Capsule フラグ                     | 0                         | システム ファームウェア プライベート capsule 更新フラグのいずれかが定義されません。                                                                                                                                                     |
|   前回の試行              | 2                         | 更新が試行された最後のシステム ファームウェアのバージョンが 2                                                                                                                                             |
|   前回の試行の状態               | 0                         | 最後のシステム ファームウェアの更新の試行は成功しました。                                                                                                                                                              |
|                                     | ファームウェア リソース エントリ 1 |                                                                                                                                                                                                                      |
|   ファームウェア クラス                    | (デバイス\_ファームウェア)        | この GUID は、デバイスのファームウェア PnP を使用して更新プログラムを識別します。                                                                                                                                                         |
|   ファームウェアの種類                     | 2                         | デバイス ファームウェアの種類には 2 です。                                                                                                                                                                                           |
|   ファームウェア バージョン                  | 1                         | 現在のデバイス ファームウェアのバージョンには 1 です。                                                                                                                                                                            |
|   サポートされているファームウェアの最小バージョン | 1                         | 1 としてサポートされているファームウェアの最小バージョンを保持します。 ファームウェアは必要な場合は 1 のバージョンにロールバックできます。                                                                                                          |
|   Capsule フラグ                     | 0x8010                    | デバイスのファームウェアは、プライベートの capsule 更新フラグ (0x8010) を定義します。                                                                                                                                                       |
|   前回の試行              | 1                         | 更新が試行された最後のデバイス ファームウェアのバージョンには 1 です。                                                                                                                                             |
|   前回の試行の状態               | 0                         | 最後のデバイス ファームウェアの更新の試行は成功しました。                                                                                                                                                              |

 

ファームウェアでは、ファームウェアのバージョンから更新プログラムを適用できませんが正常に、ESRT のエントリの最後の試行のバージョンと最後の試行ステータスは、更新が失敗した試行を反映します。 システムのバージョン 2 のファームウェアのバージョン 1 を更新しようとできない場合が正常に更新し、ファームウェアのバージョンの適用など、1、前回の試行を = = 2、および前回の試行の状態! = 0。 (つまり前回の試行の状態からためエラーが発生したことを示すゼロ以外の適切なエラー コードに設定されます。 このエントリの有効なエラー コードの一覧で、次を参照してください。 [ESRT テーブル定義](esrt-table-definition.md)します。

標準の更新ポリシーを掛けますファームウェアのバージョンを増加のみ実行できますが、以下のセクション「ロールバックしてファームウェアの更新プログラム」」の説明に従って、ポリシー設定を使用して、テスト目的でこのポリシーを無効にできます。

## <a name="system-reset"></a>システムのリセット


システムのリセットには、工場出荷時設定に戻す、システムを元に戻すにエンドユーザーことができます。 製造プロセス中にシステムにプレインストールされている Windows イメージを再インストールすることで、これを実現します。 ドライバーとアプリケーションを含め、OS 全体が再インストールされます。

**注**  セキュリティの境界を越えてファームウェアにロールバックすることを防止セキュリティ要件のためのシステムのリセットは、ファクトリにデプロイされている元のファームウェアを一致するようにファームウェアのバージョンをロールバックできるされません。 つまり、そのプラットフォームに組み込まれていたすべてのドライバーとオペレーティング システムのバージョンとの下位互換性のファームウェアのすべてのバージョンである必要があります。 ファームウェアに互換性がない場合、製造元に、システムを返すユーザー、この可能性があります。

 

## <a name="rolling-back-firmware-updates"></a>更新プログラムのファームウェアをロールバックしています


場合によっては、ファームウェアを更新などの更新プログラムのテスト中にロールバックする必要があります。 ファームウェアのリソースは、次のレジストリ キー エントリを持つ各 ESRT が報告されます。HKLM\\システム\\CurrentControlSet\\コントロール\\FirmwareResources します。

エントリで、ESRT でリソースを報告するために使用する guid と一致する名前、キーです。 ファームウェアのロールバックを許可するには、作成、REG\_DWORD 値を選択し、ポリシーと呼ばれる値を 1 に設定します。 それぞれ最小サポートされているファームウェアのバージョン、ESRT で指定されている、ファームウェアの特定のリソースをロールバックにのみできます。 これは、ファームウェアへを重要なセキュリティ修正プログラムが確立した時点より前のファームウェアのロールバックを防止します。 ファームウェアのバージョンにロールバックするこれらの条件を満たしている場合、OS ローダーは、以前のバージョンに更新されます。

## <a name="related-topics"></a>関連トピック
[ESRT テーブルの定義](esrt-table-definition.md)  
[プラグ アンド プレイ デバイス](plug-and-play-device.md)  
[更新プログラムのドライバー パッケージの作成](authoring-an-update-driver-package.md)  
[更新プログラムの処理](processing-updates.md)  
[UEFI 環境からデバイス I/O](device-i-o-from-the-uefi-environment.md)  
[シームレスな危機防止と回復](seamless-crisis-prevention-and-recovery.md)  



