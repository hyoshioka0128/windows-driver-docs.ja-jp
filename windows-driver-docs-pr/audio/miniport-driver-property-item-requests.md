---
title: ミニポート ドライバーのプロパティ項目を要求
description: ミニポート ドライバーのプロパティ項目を要求
ms.assetid: 37baad27-539b-46ab-b300-175bc0c2b992
keywords:
- プロパティ項目 WDK DirectMusic を要求します。
- ミニポート ドライバー WDK オーディオ、プロパティ項目の要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b08e4e2741f112ed684a2f9a69936ffaa29c378
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537793"
---
# <a name="miniport-driver-property-item-requests"></a>ミニポート ドライバーのプロパティ項目を要求


## <span id="miniport_driver_property_item_requests"></span><span id="MINIPORT_DRIVER_PROPERTY_ITEM_REQUESTS"></span>


このセクションでは、DirectMusic プロパティ項目の要求を簡単に紹介します。 これと他のカーネル ストリーミングの概念の概要が記載[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff560842)します。

DirectMusic ミニポート ドライバーを処理する必要があります[オーディオ ドライバーのプロパティ セット](https://msdn.microsoft.com/library/windows/hardware/ff536197)します。 2 つの部分プロパティ要求を受信します。 最初の部分は、プロパティ セットで定義されている、 [ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)構造体。 2 つ目は、プロパティ項目に固有のインスタンス データを格納するデータ バッファーです。

KSPROPERTY 構造体には、次のものが含まれています。

-   定義済みのセットを指定する GUID (など[KSPROPSETID\_シンセサイザー\_Dls](https://msdn.microsoft.com/library/windows/hardware/ff537488))。

-   セット内のプロパティ項目を指定する項目の ID (など[ **KSPROPERTY\_シンセサイザー\_DLS\_ダウンロード**](https://msdn.microsoft.com/library/windows/hardware/ff537396))。

-   要求された操作を指定するフラグ。

**フラグ**KSPROPERTY のメンバーには、ミニポート ドライバーの要求された操作を指定する、次のフラグの 1 つだけ含めることができます。

<span id="KSPROPERTY_TYPE_GET"></span><span id="ksproperty_type_get"></span>KSPROPERTY\_型\_取得  
指定したプロパティ項目の値を取得します。

<span id="KSPROPERTY_TYPE_SET"></span><span id="ksproperty_type_set"></span>KSPROPERTY\_型\_設定  
指定したプロパティ項目の値を設定します。

<span id="KSPROPERTY_TYPE_BASICSUPPORT"></span><span id="ksproperty_type_basicsupport"></span>KSPROPERTY\_型\_BASICSUPPORT  
プロパティ セットの使用可能なサポートの種類を確認します。 返されるデータ *\*pvPropertyData* KSPROPERTY の一方または両方を含む dword\_型\_GET および KSPROPERTY\_型\_を示す設定します。操作は可能です。

プロパティ項目の要求の 2 番目の部分は、ミニポート ドライバーとの間のデータを渡すために使用できるバッファーには、インスタンス データです。 このバッファーの使用方法はセットまたは GET を要求しているかに依存します。

-   要求が、KSPROPERTY 場合\_型\_設定すると、インスタンス データ、ミニポート ドライバーに送信されますが、要求元には返されません。

-   要求が、KSPROPERTY 場合\_型\_データのミニポート ドライバーで記入し、要求元に返されるインスタンスを取得します。

ミニポート ドライバー トポロジでは、特定のノードには、プロパティ項目の要求を送信できます。 ミニポート ドライバーのトポロジでは、ドライバーと基になるハードウェアのレイアウトについて説明します。 暗証番号 (pin) インスタンスが使用可能な要求の時点であるかどうか、トポロジ内ではプロパティの項目を送信するノードを指定できます。

DirectMusic 再生の暗証番号 (pin) のインスタンスを作成する必要があります。 DirectMusic データ型のノードに送信[ **KSNODETYPE\_DMSYNTH**](https://msdn.microsoft.com/library/windows/hardware/ff537167)します。 ミニポート ドライバーの接続の例を次に示します。

-   シンセサイザーにストリームに接続します。

    PCFILTER\_ノード ピン 0 (送信) -&gt; (in) は、ノード 0 ピン 1

-   シンセサイザー オーディオ出力に接続します。

    ノード 0 ピン 0 (送信) -&gt; PCFILTER\_(in) ノードの暗証番号 (pin) 1

サポートされているデータ形式は、pin の形式を指定するデータ範囲内のデータを受信できます。

DirectMusic 形式 (静的\_KSDATAFORMAT\_サブタイプ\_DIRECTMUSIC) DirectMusic ミニポート ドライバーにそのデータを送信できるように、ミニポート ドライバーのトポロジで定義する必要があります。 この形式は、DMU\_EVENTHEADER 構造 (Microsoft Windows SDK のドキュメントを参照してください) dmusbuff.h でします。 ミニポート ドライバーでは、この特定のデータ範囲をサポートしていることを指定します、DirectMusic は (ポート自体でピン留め) を介してユーザーにそのデータ範囲を公開できます。

 

 




