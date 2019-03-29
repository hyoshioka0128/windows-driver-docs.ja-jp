---
title: ヘッダー データの分割のアーキテクチャ
description: ヘッダー データの分割のアーキテクチャ
ms.assetid: a2594360-cbac-4f77-840a-2572a2381646
keywords:
- ヘッダー データの分割 WDK、アーキテクチャ
- ヘッダー データ プロバイダー WDK の分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3c4360f78c06d16486a52c7e8768ba31cd323d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573290"
---
# <a name="header-data-split-architecture"></a>ヘッダー データの分割のアーキテクチャ





ヘッダー データの分割プロバイダーでは、ヘッダーと受信のイーサネット フレーム内のデータを別のバッファーに分割することでネットワークのパフォーマンスが向上します。 ヘッダー データ プロバイダーを分割するにはには、ネットワーク インターフェイス カード (NIC) と NDIS 6.1 または NIC の services 以降のバージョンのミニポート ドライバーが含まれています。

ヘッダー データが分割されたアーキテクチャの図は、次のとおりです。

![分割されたアーキテクチャのヘッダー データを示す図](images/hdsplitarchitecture.png)

ミニポート ドライバーでは、ヘッダー データの分割操作の受信用に NIC を設定する NDIS から構成情報を受け取ります。 また、ミニポート ドライバーは、送信および受信操作などの実行時の操作、NDIS、NIC のサービスを公開します。

ヘッダー データの分割操作の対応している NIC イーサネット フレームを受信して、ヘッダーを分割し、データを別の受信バッファー。

通常の NDIS ミニポート ドライバー使用には、NDIS に受信したデータを示す関数が表示されます。 また、ドライバーを割り当てる必要があります 1 つだけ[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体を[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造を示す場合にデータを受信しました。 詳細については、次を参照してください。[受信イーサネット フレームのことを示す](indicating-received-ethernet-frames.md)します。

ヘッダー データの分割、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)受信インジケーターの構造は、記述子のヘッダー (MDLs) を一覧表示する別のメモリを使用して、受信したイーサネット フレームを分割し、データ。 また、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造に含まれるヘッダー データについては、.NET での分割\_バッファー\_情報を一覧表示します。

次の図は、受信したフレーム、分割バッファー、およびヘッダーのバッファーのメモリ レイアウトを示します。

![受信したフレーム、分割バッファー、およびヘッダーのバッファーのメモリ レイアウトを示す図](images/hdspllitbuffers.png)

ヘッダーのバッファーを連続したブロック記憶域にすべてあります。

*上位層プロトコル*は TCP、UDP、ICMP などの IP トランスポート プロトコルです。

**注**  IPsec は、ヘッダー データの分割の要件を定義するための上位層プロトコルをしないと見なされます。 IPsec のフレームの分割の詳細については、次を参照してください。 [IPsec フレームの分割](splitting-ipsec-frames.md)します。

 

 

 





