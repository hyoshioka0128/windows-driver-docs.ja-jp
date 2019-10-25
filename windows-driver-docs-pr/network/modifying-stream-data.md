---
title: ストリーム データの変更
description: ストリーム データの変更
ms.assetid: 8f591bc1-272c-4e53-8e49-3350c6a3a33e
keywords:
- コールアウトの分類 WDK Windows フィルタリングプラットフォーム、ストリームデータの変更
- データ変更のストリーミング (WDK Windows Filtering Platform)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdf6fbcb0068343e458bfe851368a737237229c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844221"
---
# <a name="modifying-stream-data"></a>ストリーム データの変更


コール[*アウトが*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)ストリームレイヤーでデータを処理する場合、データストリーム内のデータを変更することができます。 コールアウトの*classid*関数は、コールアウト関数によって、ストリーム内の許容されるデータが変更なしで渡され、削除されるストリーム内のデータをブロックし、適切なときに新しいデータまたは変更されたデータをストリームに挿入することを許可します。

コールアウトは、交換されるデータをブロックすることによって、ストリーム内のデータを他のデータに置き換えることができます。同時に、ストリームに新しいデータが挿入されます。 このような状況では、ブロックされたデータがストリームから削除されるのと同じ位置に、新しいデータがストリームに挿入されます。

データストリームにデータを挿入するためにコールアウトドライバーを使用するには、最初に挿入ハンドルを作成する必要があります。 これは、変更されたパケットデータをネットワークスタックに挿入するために作成される挿入ハンドルと同じものにすることができます。 挿入ハンドルの作成方法については[、「パケットおよびストリームデータの検査](inspecting-packet-and-stream-data.md)」を参照してください。

ストリームデータを変更する方法の詳細については、「[ハードウェアのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)コードギャラリー」の「Windows Filtering Platform Stream Edit Sample」を参照してください。

 

 





