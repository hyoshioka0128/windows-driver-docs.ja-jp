---
title: リムーバブル子デバイスの処理
description: リムーバブル子デバイスの処理
ms.assetid: 0edc0331-7178-4986-b818-9f1ee8f12995
keywords:
- Windows 2000 の WDK の子のリムーバブル デバイスを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29da5f07e151903207d661bac859c9b7cca7bc70
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359321"
---
# <a name="handling-removable-child-devices"></a>リムーバブル子デバイスの処理


ビデオのミニポート ドライバーをドライバーがプラグ アンド プレイ (PnP) を防ぐため、元の子デバイスのデータを使用してから、デバイスなどの別の子のリムーバブル デバイスが変更されたときに検出する必要があります。 たとえば、ビデオのミニポート ドライバーでは、ユーザーは、モニターを切り替えたときを検出する必要があります。

ビデオのミニポート ドライバーの連続する呼び出しの間で拡張表示情報 Data (EDID) に接続しているモニターが変更された場合[ *HwVidGetVideoChildDescriptor* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)解除を行うのではなく、関数元のモニター スタックと新しいモニターの新しいスタックを構築、ダウン ビデオ ポート ドライバーは、現在のスタックの状態を変更します。 他のオペレーティング システム コンポーネントを元のスタックが破損しないため、グラフィックス サブシステムで新しいモニターの機能を確認できます (次のように、PnP) 元のモニターの機能のデータを使用します。

ビデオのミニポート ドライバーでは、接続しているモニターへの変更を検出および PnP から元のモニターのデータを使用するようにするのには、次の操作のいずれかを実行できます。

1.  ビデオのミニポート ドライバーでは、モニターが前者モニター スタックのダウン、終了処理を強制するために存在しないことを報告できます。 次を強制的に再新しいモニターをレポートするには子デバイスを列挙するビデオ ポート ドライバー、ビデオのミニポート ドライバー呼び出し、 [ **VideoPortEnumerateChildren** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportenumeratechildren)関数。 ビデオのミニポート ドライバーを呼び出す必要があります**VideoPortEnumerateChildren**が完了すると、モニターが切断されていることを報告する最初の列挙体の後にのみ再列挙子デバイスのスケジュールを設定します。

2.  適切なコンピューターとモニターの構成 (次の例外を参照してください) では、ビデオのミニポート ドライバーに応答できるその*HwVidGetVideoChildDescriptor*変数で新しいモニターを*UId*パラメーターを指します。 この値は、元のモニターのビデオのミニポート ドライバーが使用される値と異なるである必要があります。

Advanced Configuration and Power Interface (ACPI) 列挙モニター最初のメカニズムである 32 ビットのデバイス Id が、BIOS の実装に関連付けられているためことをお勧めします。 そのため、別の 32 ビットのデバイスを指定する ID できない可能性があります。

 

 





