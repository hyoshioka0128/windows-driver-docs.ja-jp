---
title: 携帯ネットワークのアーキテクチャと実装
description: Windows 10 用の携帯電話のアーキテクチャには、Windows 8.1 と Windows Phone 8.1 の両方から要素が含まれています。
ms.assetid: A6F23D12-BCF0-496A-B881-C1F6B35EDA4D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddccf6beed7f381f52ed29c9a02f4bb18325d66d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345339"
---
# <a name="cellular-architecture-and-implementation"></a>携帯ネットワークのアーキテクチャと実装


Windows 10 用の携帯電話のアーキテクチャには、Windows 8.1 と Windows Phone 8.1 の両方から要素が含まれています。 以下には、新しい Windows 10 のアーキテクチャ ダイアグラムと実装する必要がある携帯電話のコンポーネントとの比較の Windows 8.1 および Windows Phone 8.1 の携帯電話のアーキテクチャの図を示します。

## <a name="windows10-architecture"></a>Windows 10 のアーキテクチャ:


![windows 10 の移動体通信アーキテクチャ](images/win10-cellular-architecture.png)

## <a name="windows10-cellular-implementation-requirements"></a>Windows 10 の携帯電話の実装要件


Windows 10 では、実装する必要がある携帯電話のコンポーネントは、デスクトップ エディションの Windows 10 Mobile デバイスが Windows 10 を使用するかどうかによって異なります。

Windows 10 デスクトップ エディションの場合、次が必要です。

-   モデムのハードウェアで MBIM プロトコル インターフェイスを実装します。
-   モデムのハードウェアに USB インターフェイスを実装します。 リムーバブル USB ドングルまたは USB ホスト コント ローラーはそれ自身を別のインターフェイスが考えられます。

Windows 10 Mobile では、次が必要です。

- IHV RIL (無線インターフェイス層) とモバイル ブロード バンド NDIS ドライバーが、モデムを実装します。
  ## <a name="windows-81-architecture"></a>Windows 8.1 のアーキテクチャ:


![windows 8.1 の携帯電話のアーキテクチャ](images/win81-cellular-architecture.png)

## <a name="windows-phone-81-architecture"></a>Windows Phone 8.1 のアーキテクチャ:


![windows phone 8.1 の携帯電話のアーキテクチャ](images/winphone81-cellular-architecture.png)


## <a name="related-topics"></a>関連トピック


[モバイル ブロード バンド (MB) の設計ガイド](mobile-broadband--mb--design-guide.md)

 

 






