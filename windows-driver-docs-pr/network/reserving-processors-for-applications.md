---
title: アプリケーションのプロセッサを予約します。
description: アプリケーションのプロセッサを予約します。
ms.assetid: e09790e9-29a7-4ff6-a122-b4bd99de8bc7
keywords:
- WDK の RSS CPU の構成
- WDK の RSS のアプリケーションのプロセッサを予約します。
- WDK の RSS のプロセッサ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ef6dfe6e40cef6cbaeb001cb38a49aa614c1b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551409"
---
# <a name="reserving-processors-for-applications"></a>アプリケーションのプロセッサを予約します。





スケーリング (RSS) インターフェイスの受信側では、管理者はアプリケーションを使用するプロセッサのセットを予約できます。 管理者は、論理 CPU 数 0 から始まると、指定した CPU 数で終了するプロセッサのセットを予約できます。 RSS *CPU 数を基本*RSS に使用できる最初の CPU の CPU の数です。 RSS は、基本の CPU 数の下の番号付けは Cpu を使用できません。 ハイパー スレッディングを無効になっているクアッド コア システムでなどの RSS プロセッサ 1、2、および 3 を使用できる CPU の基数が 1 に設定されている場合。

NDIS が基本の CPU 数の既定値の 0 を使用しますが、管理者は、この値を変更できます。 RSS インターフェイスには、連続していない、任意のアプリケーションを使用するための Cpu のサブセットを予約するには、管理者許可されていません。

Microsoft Windows Server 2003 Scalable Networking Pack で、管理者を設定できますベース CPU 番号、 **RssBaseCpu**レジストリ キーワード**HKEY\_ローカル\_マシン\\\\システム\\CurrentControlSet\\サービス\\Tcpip\\パラメーター**します。 **RssBaseCpu**値は DWORD 型であり、NDIS が 0 の既定値を使用してが存在しない場合。

Windows Server 2008 では、管理者を設定できますベース CPU 番号、 **RssBaseCpu**レジストリ キーワード**HKEY\_ローカル\_マシン\\\\システム\\CurrentControlSet\\サービス\\NDIS\\パラメーター**します。 **RssBaseCpu**値は DWORD 型であり、NDIS が 0 の既定値を使用してが存在しない場合。 このレジストリ キーワードは、以降のバージョンの Windows Server にも適用されます。

**注**以降 Windows 8 および Windows Server 2012 では、管理者は制御できますに多くのネットワーク アダプターの PowerShell コマンドレットを使用します。 レジストリを直接編集することは推奨されませんようになりました。

RSS Cpu を予約するための PowerShell コマンドレットは[Set-netadapterrss](https://technet.microsoft.com/library/jj130863)します。 使用しての主な違い**Set-netadapterrss**を使用して、 **RssBaseCpu**中 - ネットワーク アダプターごとに PowerShell コマンドレットが動作するは**RssBaseCpu**つまり、すべてのネットワーク アダプターに適用される、グローバルです。 一般に、個別に各ネットワーク アダプターの使用はお勧め詳細の柔軟性、粒度と各ネットワーク アダプターを付与するには、独自の構成か。 ただし、管理者は、グローバルと使用も**RssBaseCpu**扱おうと同時にすべての現在および今後のすべてのネットワーク アダプターに構成を適用する場合のキーします。

ネットワーク アダプター コマンドレットの完全な一覧を参照してください。 [Windows PowerShell のネットワーク アダプター コマンドレット](https://technet.microsoft.com/library/jj134956)します。

 

 





