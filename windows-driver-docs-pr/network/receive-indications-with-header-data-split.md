---
title: ヘッダー データ分割による受信表示
description: ヘッダー データ分割による受信表示
ms.assetid: 76abeac8-ca6e-40b1-a46e-83ae90d9192e
keywords:
- WDK の分割、インジケーターが表示されるデータをヘッダー
- 受信したデータ形式 WDK ヘッダー以外のデータの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f80b5080b65240207389376940298bc170913ca3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385011"
---
# <a name="receive-indications-with-header-data-split"></a>ヘッダー データ分割による受信表示





ヘッダー データの分割を示す必要がありますをサポートしていますがヘッダー データの分割の形式でデータを受信したミニポート ドライバーが必要です。 たとえば、ヘッダーのバッファーはすべてストレージの連続したブロック内にし、データ バッファーはバックフィル スペースを含める必要があります。

分割フレームのヘッダー情報は、仮想 LAN (VLAN) タグを含めることはありません必要があります。 ヘッダー データの分割がハードウェアで VLAN のサポートが必要ですし、着信フレームから VLAN タグを削除して、内に配置することが必要です、 **Ieee8021QNetBufferListInfo**で OOB 情報、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 ミニポート ドライバーで VLAN のサポートを指定する必要があります、 **MacOptions**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性** ](https://msdn.microsoft.com/library/windows/hardware/ff565923)構造体に応答して、 [OID\_GEN\_MAC\_オプション](https://msdn.microsoft.com/library/windows/hardware/ff569597)OID クエリ。

NDIS と関連付けたドライバーまたはユーザー モード アプリケーションを使用して、 [OID\_GEN\_HD\_分割\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569587)現在のヘッダー データを設定する OID ミニポート アダプターの設定を分割します。 場合は、NDIS\_HD\_分割\_結合\_すべて\_ヘッダー フラグ、 **HDSplitCombineFlags**のメンバー、 [ **NDIS\_HD\_分割\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565701)構造が設定されている、ミニポート アダプターが分割のすべてのフレームを結合する必要があります。 ヘッダー データの分割が有効で、ハードウェアの場合、ミニポート ドライバーは、NDIS フレームを示す前に、ヘッダーとデータを組み合わせる必要があります。 OID の詳細については\_GEN\_HD\_分割\_パラメーターとその他の管理と構成の問題を参照してください[ヘッダー データの分割の管理と構成](header-data-split-administration-and-configuration.md).

このセクションの内容:

[ヘッダーのバッファーを割り当てる](allocating-the-header-buffer.md)

[バックフィルをデータ バッファーの割り当てください。](allocating-backfill-for-the-data-buffer.md)

[NET の設定\_バッファー\_情報を一覧表示](setting-net-buffer-list-information.md)

 

 





