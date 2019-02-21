---
title: UPS ミニドライバーの書き込み
description: UPS ミニドライバーの書き込み
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
ms.openlocfilehash: 88a19094bacda3114155c76f70eba10bc7b30870
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539530"
---
# <a name="writing-ups-minidrivers"></a>UPS ミニドライバーの書き込み


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

**注**   Windows Vista 以降のバージョンの Windows では、COM ポートに接続されている ups をサポートしていません。 Ups を経由して接続をサポートするためにこれらの Windows のバージョンが引き続き[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)します。

 

 

 




