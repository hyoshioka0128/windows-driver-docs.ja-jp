---
title: UPS ミニドライバーの作成
description: UPS ミニドライバーの作成
ms.assetid: 85142cbf-cb3b-4ccf-a005-8fcb7a7ad12b
keywords:
- UPS ミニドライバー WDK
- 単純なシグナリング WDK
- スマート シグナリング WDK
- UPS サービス WDK
- システム提供の UPS サービス WDK
- UPS ミニドライバー WDK、UPS ミニドライバーの記述について
- 無停電電源装置 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfa4cc4cd7f1cfef40ac34d4f5a3d5f5e3142679
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355239"
---
# <a name="writing-ups-minidrivers"></a>UPS ミニドライバーの作成


## <span id="ddk_writing_ups_minidrivers_kg"></span><span id="DDK_WRITING_UPS_MINIDRIVERS_KG"></span>


無停電電源装置 (UPS) が、Microsoft Windows システムに接続されている場合、 **UPS**タブ**電源オプション**コントロール パネルの UPS に関する情報を提供します。 Windows Server 2003、Windows XP、および Windows 2000 では、システム提供の UPS サービスは、非常に限定された管理機能およびステータス情報を提供する COM ポートとそのサポート「単純なシグナル型、」に接続されている UPS 装置のサポートをします。

Windows Server 2003、Windows XP、および Windows 2000、UPS のモデルが COM ポートに接続されている「スマート シグナル、」をサポートしている場合と、次の UPS ミニドライバーが提供する必要があります。 このミニドライバーは、ユーザー モード DLL では、システムの UPS サービスによって呼び出されると、次の操作を実行します。

-   UPS への通信パスを初期化します。

-   レジストリ エントリを更新する**電源オプション**を使用して表示するモデルに固有の情報を取得します。

-   要求時に UPS の電源をオフにします。

-   UPS ユニットの状態の変更を監視します。

UPS ミニドライバーの詳細については、次のトピックを参照してください。

[UPS ミニドライバー機能](ups-minidriver-functionality.md)

[UPS レジストリ エントリ](ups-registry-entries.md)

[UPS ミニドライバーをサンプルします。](sample-ups-minidriver.md)

[UPS ミニドライバーをインストールします。](installing-ups-minidrivers.md)

**注**   Windows Vista 以降のバージョンの Windows では、COM ポートに接続されている ups をサポートしていません。 Ups を経由して接続をサポートするためにこれらの Windows のバージョンが引き続き[USB](https://docs.microsoft.com/windows-hardware/drivers/)します。

 

 

 




