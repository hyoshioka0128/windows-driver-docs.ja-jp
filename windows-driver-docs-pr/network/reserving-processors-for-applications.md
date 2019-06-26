---
title: アプリケーション用のプロセッサの予約
description: アプリケーション用のプロセッサの予約
ms.assetid: e09790e9-29a7-4ff6-a122-b4bd99de8bc7
keywords:
- WDK の RSS CPU の構成
- WDK の RSS のアプリケーションのプロセッサを予約します。
- WDK の RSS のプロセッサ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23fb0637dc6663d4e88821c2932d80f880550fc7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378654"
---
# <a name="reserving-processors-for-applications"></a>アプリケーション用のプロセッサの予約





スケーリング (RSS) インターフェイスの受信側では、管理者はアプリケーションを使用するプロセッサのセットを予約できます。 管理者は、論理 CPU 数 0 から始まると、指定した CPU 数で終了するプロセッサのセットを予約できます。 RSS *CPU 数を基本*RSS に使用できる最初の CPU の CPU の数です。 RSS は、基本の CPU 数の下の番号付けは Cpu を使用できません。 ハイパー スレッディングを無効になっているクアッド コア システムでなどの RSS プロセッサ 1、2、および 3 を使用できる CPU の基数が 1 に設定されている場合。

NDIS が基本の CPU 数の既定値の 0 を使用しますが、管理者は、この値を変更できます。 RSS インターフェイスには、連続していない、任意のアプリケーションを使用するための Cpu のサブセットを予約するには、管理者許可されていません。

Microsoft Windows Server 2003 Scalable Networking Pack で、管理者を設定できますベース CPU 番号、 **RssBaseCpu**レジストリ キーワード**HKEY\_ローカル\_マシン\\\\システム\\CurrentControlSet\\サービス\\Tcpip\\パラメーター**します。 **RssBaseCpu**値は DWORD 型であり、NDIS が 0 の既定値を使用してが存在しない場合。

Windows Server 2008 では、管理者を設定できますベース CPU 番号、 **RssBaseCpu**レジストリ キーワード**HKEY\_ローカル\_マシン\\\\システム\\CurrentControlSet\\サービス\\NDIS\\パラメーター**します。 **RssBaseCpu**値は DWORD 型であり、NDIS が 0 の既定値を使用してが存在しない場合。 このレジストリ キーワードは、以降のバージョンの Windows Server にも適用されます。

**注**以降 Windows 8 および Windows Server 2012 では、管理者は制御できますに多くのネットワーク アダプターの PowerShell コマンドレットを使用します。 レジストリを直接編集することは推奨されませんようになりました。

RSS Cpu を予約するための PowerShell コマンドレットは[Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss)します。 使用しての主な違い**Set-netadapterrss**を使用して、 **RssBaseCpu**中 - ネットワーク アダプターごとに PowerShell コマンドレットが動作するは**RssBaseCpu**つまり、すべてのネットワーク アダプターに適用される、グローバルです。 一般に、個別に各ネットワーク アダプターの使用はお勧め詳細の柔軟性、粒度と各ネットワーク アダプターを付与するには、独自の構成か。 ただし、管理者は、グローバルと使用も**RssBaseCpu**扱おうと同時にすべての現在および今後のすべてのネットワーク アダプターに構成を適用する場合のキーします。

ネットワーク アダプター コマンドレットの完全な一覧を参照してください。 [Windows PowerShell のネットワーク アダプター コマンドレット](https://docs.microsoft.com/powershell/module/netadapter/)します。

 

 





