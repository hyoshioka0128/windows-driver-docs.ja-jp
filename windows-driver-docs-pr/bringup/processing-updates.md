---
title: 更新プログラムの処理
description: Windows OS ローダーは、ファームウェアの更新パッケージが適用されていると、システムの再起動後、ファームウェアのペイロードのすべてのファイルを読み込みます (この例で firmware.bin) 物理メモリにします。
ms.assetid: 87BC1366-F69D-412A-883E-861853A4902A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5b554d462080271a0886272ccbeed1a09d57d33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571508"
---
# <a name="processing-updates"></a>更新プログラムの処理


Windows OS ローダーは、ファームウェアの更新パッケージが適用されていると、システムの再起動後、ファームウェアのペイロードのすべてのファイルを読み込みます (この例で*firmware.bin*) 物理メモリにします。 Windows OS ローダーは、各更新の対応する ESRT エントリから、UEFI UpdateCapsule を呼び出すときに使用するには、GUID とフラグを記述する情報を使用して capsule のヘッダーを作成します。 Capsule ヘッダーの flags フィールドを設定するには、Windows OS ローダー、常に設定 CAPSULE\_フラグ\_PERSIST\_ACROSS\_リセットと CAPSULE\_フラグ\_開始\_リセットします。 Windows OS ローダーは CAPSULE を設定してさらに\_フラグ\_POPULATE\_システム\_ファームウェアのテーブル型デバイス\_ファームウェア、ドライバー パッケージの INF で capsule フラグが指定されている場合。 さらに、フラグを指定して、INF で指定できますも独自の capsule が含められます UEFI UpdateCapsule を呼び出すときに

ESRT 例を参照する[ESRT テーブル定義](esrt-table-definition.md)とのファームウェア リソース更新のドライバー パッケージ INF 例[update のドライバー パッケージの作成](authoring-an-update-driver-package.md)、capsule ヘッダー Windows OS ローダー作成します UpdateCapsule にパスに次のようになります。

| フィールド            | 値              | Comment                                                 |
|------------------|--------------------|---------------------------------------------------------|
| CapsuleGuid      | {0} システム\_ファームウェア} | 対応する ESRT からリソース エントリの FirmwareClass します。 |
| HeaderSize       | …                  | 固定 ページに埋め込まれる*firmware.bin*を開始します。              |
| フラグ            | 0x50000            | 間で、永続化の開始しリセットします。                    |
| CapsuleImageSize | …                  | ヘッダーのサイズ + のサイズを capsule *firmware.bin*します。       |

 

この例の ESRT で定義されている 2 つのデバイスの 1 つだけでテーブルがインストールされていること、新しいファームウェア リソース更新のドライバー パッケージに注意してください。 ファームウェア リソースの更新プログラムのドライバー パッケージは、表 2 の 2 つ目のデバイス用に作成され対応するファームウェア リソース デバイスにインストールし場合、2 番目の capsule ヘッダーはよう作成は。

| フィールド            | [値]              | Comment                                                                                                                                 |
|------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| CapsuleGuid      | {0} デバイス\_ファームウェア} | 対応する ESRT からリソース エントリの FirmwareClass します。                                                                                 |
| HeaderSize       | …                  | デバイスのページ揃えにするには、埋め込まれます。箱を開始します。                                                                                                  |
| フラグ            | 0x50000            | 間で、永続化し開始、リセット、およびシステム テーブルを作成または対応する ESRT から 0x8010 とリソース エントリの CapsuleFlags します。 |
| CapsuleImageSize | …                  | Capsule のヘッダーのサイズ + デバイスのサイズ。ビン。                                                                                           |

 

Windows OS ローダーがすべての保留中のファームウェアの更新プログラムが読み込まれ、説明のために必要なデータ構造を作成、その後 ExitBootServices を呼び出す前に、UpdateCapsule ランタイム サービスを呼び出します。

**注**  プラットフォーム ファームウェアがある対応する記憶域デバイスを含むすべてのデバイスの排他的制御ときに、UpdateCapsule が ExitBootServices する前に呼び出されます。 UpdateCapsule のプラットフォーム ファームウェアの実装は、更新プログラムを段階的にまたは回復ロールバックをサポートする永続的ストレージにファームウェア更新プログラムのペイロードを保存できます。

 

## <a name="related-topics"></a>関連トピック
[ESRT テーブルの定義](esrt-table-definition.md)  
[プラグ アンド プレイ デバイス](plug-and-play-device.md)  
[更新プログラムのドライバー パッケージの作成](authoring-an-update-driver-package.md)  
[UEFI 環境からデバイス I/O](device-i-o-from-the-uefi-environment.md)  
[シームレスな危機防止と回復](seamless-crisis-prevention-and-recovery.md)  
[ファームウェアの更新状態](firmware-update-status.md)  



