---
title: 機内モード無線管理
description: Windows 8 以降、Windows オペレーティング システムは、HID を介した機内モード無線管理コントロールのサポートを提供します。
ms.assetid: 5B0662B0-CBD3-4F31-B98F-6BC8184574DB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c55bdac9dd253b236aa95afe77b07d5cfbc08b18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528396"
---
# <a name="airplane-mode-radio-management"></a>機内モード無線管理


Windows 8 以降、Windows オペレーティング システムは、HID を介した機内モード無線管理コントロールのサポートを提供します。

## <a name="architecture-and-overview"></a>アーキテクチャと概要


機内モードの目的は、ボタンを提供する PC の製造元を許可するまたはスイッチ (と可能性のある状態を示す LED) エンドユーザーがオン/オフを一度にすべてのワイヤレス コントロールできるようにします。 これは主にでソフトウェアを使用してラジオをワイヤレスさまざまなオペレーティング システムを許可するプログラムによる方法 (a) スイッチおよび (b) のコントロールの状態を識別するために、機内モードをオン/オフにする必要があるユーザーを支援します。

Windows では、Generic Desktop の [使い方] ページで、次の HID の使用のサポートを提供します。

| 使用状況 ID | 使用法の名前                   | 使用法の種類                 |
|----------|------------------------------|----------------------------|
| 0x000C   | ワイヤレス通信 Controlls     | CollectionApplication (CA) |
| 0x00C6   | ワイヤレスのラジオ ボタン        | コントロール (OOC) のオン/オフ       |
| 0x00C7   | 無線 LED           | コントロール (OOC) のオン/オフ       |
| 0x00C8   | ワイヤレス通信スライダー スイッチ | コントロール (OOC) のオン/オフ       |

 

ラジオの管理のサポートを提供する HID クライアントのアーキテクチャの図を次に示します/機内モード。

![機内モード アーキテクチャ](images/airplane-mode.png)

ShellHW 検出サービス (SHSVCD.dll) は、HID クライアント ドライバー/サービス ユーザー モードで実行され、無線管理デバイスのサポートを提供します。 型の非表示にコレクションの上位レベルの存在を監視します。

-   使用状況\_ページ (Generic Desktop) 05 01
-   使用状況 (ワイヤレス コントロール) 09 0 C

## <a name="sample-report-descriptor"></a>サンプル レポート記述子


次のセクションで、サンプル レポート記述子の PC の製造元を活用する必要があります。 上位レベルのコレクションが別の上位レベルのコレクションに既にレポート記述子の一部である場合は、必要がありますレポート ID 含まれること (以下のサンプルでは表示されません) に注意してください。

次のセクションでは、PC 製造元向け追加情報を提供し、どのレポート記述子のサンプルは、システムの設計に最も適したを識別します。

-   コンシューマー コントロール ボタンのキーボードでステートレスなボタンを使用して多くの場合、(スタンドアロンまたは多くのモバイル システム (例: Fn + F5)、関数ボタンと組み合わせて)。
-   スライダーのスイッチは、モバイル システムの物理のスライダーをオン/オフ スイッチ (例: スイッチのオン/オフを機内モードとラップトップ) でよく使用されます。
-   LED は、多くの場合、スタンド アロン飛行機として複数のインジケーターを使用またはスイッチと組み合わせて、ステートレスなボタンまたはスライダーにします。 ウィンドウのユーザーでは、機内モードを UI に表示されるモバイル フォーム ファクターのシステムでこの LED の使用を必要はありません。

*LED せずステートレス ボタン*

``` syntax
USAGE_PAGE (Generic Desktop)                   05 01 
USAGE (Wireless Radio Controls)                09 0C 
COLLECTION (Application)                       A1 01 
LOGICAL_MINIMUM (0)                            15 00 
LOGICAL_MAXIMUM (1)                            25 01 
USAGE (Wireless Radio Button)                  09 C6 
REPORT_COUNT (1)                               95 01 
REPORT_SIZE (1)                                75 01 
INPUT (Data,Var,Rel)                           81 06 
REPORT_SIZE (7)                                75 07 
INPUT (Cnst,Var,Abs)                           81 03 
END_COLLECTION                                 C0
```

*LED とステートレスのボタン*

``` syntax
USAGE_PAGE (Generic Desktop)                    05 01 
USAGE (Wireless Radio Controls)                 09 0C 
COLLECTION (Application)                        A1 01 
LOGICAL_MINIMUM (0)                             15 00 
LOGICAL_MAXIMUM (1)                             25 01 
USAGE (Wireless Radio Button)                   09 C6 
REPORT_COUNT (1)                                95 01 
REPORT_SIZE (1)                                 75 01 
INPUT (Data,Var,Rel)                            81 06 
REPORT_SIZE (7)                                 75 07 
INPUT (Cnst,Var,Abs)                            81 03 
USAGE (Wireless Radio LED)                      09 C7 
REPORT_SIZE (1)                                 75 01 
OUTPUT (Data,Var,Rel)                           91 02 
REPORT_SIZE (7)                                 75 07 
OUTPUT (Cnst,Var,Abs)                           91 03 
END_COLLECTION                                  C0
```

*スライダーのスイッチ (LED) なし*

``` syntax
USAGE_PAGE (Generic Desktop)                    05 01 
USAGE (Wireless Radio Controls)                 09 0C 
COLLECTION (Application)                        A1 01 
LOGICAL_MINIMUM (0)                             15 00 
LOGICAL_MAXIMUM (1)                             25 01 
USAGE (Wireless Radio Slider Switch)            09 C8 
REPORT_COUNT (1)                                95 01 
REPORT_SIZE (1)                                 75 01 
INPUT (Data,Var,Abs)                            81 02 
REPORT_SIZE (7)                                 75 07 
INPUT (Cnst,Var,Abs)                            81 03 
END_COLLECTION                                  C0
```

*スライダー スイッチと LED*

``` syntax
USAGE_PAGE (Generic Desktop)                    05 01 
USAGE (Wireless Radio Controls)                 09 0C 
COLLECTION (Application)                        A1 01 
LOGICAL_MINIMUM (0)                             15 00 
LOGICAL_MAXIMUM (1)                             25 01 
USAGE (Wireless Radio Slider Switch)            09 C8 
REPORT_COUNT (1)                                95 01 
REPORT_SIZE (1)                                 75 01 
INPUT (Data,Var,Abs)                            81 02 
REPORT_SIZE (7)                                 75 07 
INPUT (Cnst,Var,Abs)                            81 03 
USAGE (Wireless Radio LED)                      09 C7 
REPORT_SIZE (1)                                 75 01 
OUTPUT (Data,Var,Rel)                           91 02 
REPORT_SIZE (7)                                 75 07 
OUTPUT (Cnst,Var,Abs)                           91 03 
END_COLLECTION                                  C0
```

*LED のみ (ボタンまたはスライダー)*

``` syntax
USAGE_PAGE (Generic Desktop)                   05 01 
USAGE (Wireless Radio Controls)                09 0C 
COLLECTION (Application)                       A1 01 
LOGICAL_MINIMUM (0)                            15 00 
LOGICAL_MAXIMUM (1)                            25 01 
USAGE (Wireless Radio LED)                     09 C7 
REPORT_COUNT (1)                               95 01 
REPORT_SIZE (1)                                75 01 
OUTPUT (Data,Var,Rel)                          91 02 
REPORT_SIZE (7)                                75 07 
OUTPUT (Cnst,Var,Abs)                          91 03 
END_COLLECTION                                 C0
```

## <a name="troubleshooting-common-errors"></a>一般的なエラーのトラブルシューティング


ヒント: \#1。ラジオ manager ボタンを使用する場合、PC の製造元は、ボタンが押されたときではなく、ボタンが離されたときと 1 つの HID レポートを送信する必要があります。 これは、入力を相対と絶対 1 ではありません、トグル ボタンが通常ためです。

ヒント: \#2。のみ、機内モード無線管理 HID の使用は、モバイル システム (電源バッテリ使用時) で動作し、Windows 8 または Windows の以降のバージョンが必要です。

ヒント: \#3。機内モード無線管理 ボタンの詳細については、次を参照してください。、[キーボードの Windows 8 の機能拡張](https://msdn.microsoft.com/library/windows/hardware/dn613956.aspx)ホワイト ペーパー。

ヒント: \#4。ボタンは、に関する詳細については、適切なハードウェアを実装するためには、Windows 8 システム ロゴの要件を確認してください。

 

 




