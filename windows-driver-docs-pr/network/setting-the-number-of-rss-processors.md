---
title: RSS プロセッサの数の設定
description: RSS プロセッサの数の設定
ms.assetid: c13db4a1-e345-4368-9bcd-afbd2fd8db7a
keywords:
- WDK の RSS のプロセッサ
- WDK の RSS CPU の構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2574fde01ad98cbc9869c40a59067de254f88f64
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375128"
---
# <a name="setting-the-number-of-rss-processors"></a>RSS プロセッサの数の設定





管理者の数を設定する必要があります、コンピューターの全体的なパフォーマンスを向上するスケーリング (RSS) のプロセッサを側を受信します。 複数の Cpu の有効化が分散で実行されている同時実行の遅延プロシージャ呼び出し (Dpc) は、受信処理し、(たとえば、高速の Nic) で CPU のボトルネックを削除します。 ただし、複数の Dpc オーバーヘッドが追加作成しないでください。 割り込みと DPC の RSS より多くのプロセッサが使用されるため、オーバーヘッドの増加を処理します。 したがって、RSS がアクティブなすべての cpu の合計 CPU 使用率が増加します。 管理者は、RSS、RSS を使用してアプリケーションを使用するためには、少ない処理能力を離れるし、ネットワーク スループットは向上しません状況を回避するために使用される Cpu の数を選択する必要があります。

Scalable Networking Pack で Microsoft Windows Server 2003 では、管理者がの RSS Cpu の最大数を設定できます、 **MaxNumRssCpus**レジストリ キーワード**HKEY\_ローカル\_マシン\\\\システム\\CurrentControlSet\\サービス\\Tcpip\\パラメーター**します。 **MaxNumRssCpus**値は DWORD 型であり、NDIS 4 の既定値を使用してが存在しない場合。

Windows Server 2008 では、管理者は RSS Cpu の最大数を設定、 **MaxNumRssCpus**レジストリ キーワード**HKEY\_ローカル\_マシン\\\\システム\\CurrentControlSet\\サービス\\Ndis\\パラメーター**します。 **MaxNumRssCpus**値は DWORD 型であり、NDIS 4 の既定値を使用してが存在しない場合。 このレジストリ キーワードは、以降のバージョンの Windows Server にも適用されます。

複雑な場合 (および実際のハードウェアで実装されていない非現実的な場合) を回避するために使用可能なハードウェアの受信キューが小さい、RSS Cpu 数よりも管理者を設定する必要がありますいない、 **MaxNumRssCpus**値を 16 よりも大きい値です。

RSS に使用される Cpu の実際の数は、RSS ベース CPU の数を構成した後に残っているコア プロセッサの合計数によっても制限されます。 などの場合は、管理者は、6 へのクアッド コア コンピューター システム上の RSS Cpu の最大数を設定、ネットワーク ドライバー スタックを使用して、多くて、RSS の 4 つの Cpu。 また、管理者は RSS ベース CPU の数を 1 に設定、ネットワーク ドライバー スタックは最大で 3 つの Cpu (CPU 番号 1、2、および 3) を使用します。

 RSS のコンピューターで使用される Cpu の数は静的であり、実行時に変更されません。 そのためへの変更、 **MaxNumRssCpus**レジストリ値を有効にする再起動が必要があります。

**注**以降 Windows 8 および Windows Server 2012 では、管理者は制御できますに多くのネットワーク アダプターの PowerShell コマンドレットを使用します。 レジストリを直接編集することは推奨されませんようになりました。 

RSS Cpu の数を設定するための PowerShell コマンドレットは[Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss)します。 使用しての主な違い**Set-netadapterrss**を使用して、 **MaxNumRssCpus**中 - ネットワーク アダプターごとに PowerShell コマンドレットが動作するは**MaxNumRssCpus**はグローバルですべてのネットワーク アダプターに適用されることを意味します。 一般に、個別に各ネットワーク アダプターの使用はお勧め詳細の柔軟性、粒度と各ネットワーク アダプターを付与するには、独自の構成か。 ただし、管理者は、グローバルと使用も**MaxNumRssCpus**扱おうと同時にすべての現在および今後のすべてのネットワーク アダプターに構成を適用する場合のキーします。

ネットワーク アダプター コマンドレットの完全な一覧を参照してください。 [Windows PowerShell のネットワーク アダプター コマンドレット](https://docs.microsoft.com/powershell/module/netadapter/)します。
