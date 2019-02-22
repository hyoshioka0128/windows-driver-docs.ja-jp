---
title: Stream クラスの子デバイス
description: Stream クラスの子デバイス
ms.assetid: 2885a77d-5e39-4730-b715-99f0a426f273
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネルが子デバイス
- ミニドライバー WDK Windows 2000 のカーネル、デバイスの子のストリーミング
- ミニドライバー WDK Windows 2000 カーネル ストリーミング、子デバイス
- 子デバイス WDK ストリーミング ミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2193cb84d3c7713ce0b74b403f4dcea1308d84f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538610"
---
# <a name="stream-class-child-devices"></a>Stream クラスの子デバイス





このセクションでは、そのプラットフォームに DirectX 9.0 以降がインストールされている場合にのみ、Microsoft Windows Server 2003 と以前のオペレーティング システムに適用されます。

Stream クラス デバイスに配置される場合、**列挙型**子デバイス内の各キーを作成する、デバイスのバス エミュレーターとして、デバイス キー、ストリーム クラスの下のレジストリ内のブランチの動作、**列挙型**分岐します。

**AddReg**ドライバーの INF ファイル、仕入先のセクションは、値を提供*pnpid*型 REG の\_にある各エントリの SZ**列挙型**します。 Stream クラスを使用してこの文字列値、プラグ アンド プレイ (PnP) を構築するハードウェア ID 個々 の子デバイスごとにします。

リリースで DirectX 9.0 より前ストリーム クラスを作成、フォームの子デバイスのハードウェア ID"AVStream\\*&lt;pnpid&gt;*"(場所&lt;pnpid&gt;の値です*pnpid*特定のデバイス)。

たとえば、仕入先がでは、次を指定します、 **AddReg** INF ファイルのセクション。

```INF
[MyTVDevice.AddReg]
HKR,"ENUM\CrossbarDevice",pnpid,,"MyCrossbar"
HKR,"ENUM\TunerDevice",pnpid,,"MyTuner"
```

したがって、ストリーム クラスでは、次のデバイス Id で 2 つの子デバイスを作成します。

Stream\\MyCrossbar

Stream\\MyTuner

同じを指定する 2 つの異なる子デバイスからであいまいさを解決するのには*pnpid*値、DirectX 9.0 と報告の各子デバイス Id を後で変更します。 親デバイスによって報告されたハードウェア id ごとに、ストリーム クラスは、次の形式の子デバイスの ID を作成します。

Stream\\*&lt;pnpid&gt;*\#*&lt;親ハードウェア ID の変更&gt;*

変更された親のハードウェア ID は、各円記号と、親のハードウェア ID (**\\**) 文字に置き換え、番号記号 (**\#**)。

ストリーム クラスに最大で ID 文字列が終了した結果の文字列が長すぎる場合\_デバイス\_ID\_LEN 文字を含む、 **NULL**ターミネータです。 Windows Server 2003 では、この制限は 200 文字で設定*cfgmgr32.h*します。

たとえば、親デバイスは、次のハードウェア Id を報告します。

PCI\\VEN\_XXXX &AMP; DEV\_YYYY &AMP; SUBSYS\_ZZZZZZZZ &AMP; REV\_VV

PCI\\VEN\_XXXX &AMP; DEV\_YYYY &AMP; SUBSYS\_ZZZZZZZZ

使用したデバイスの*pnpid*のキー **MyCrossbar**、ストリーム クラスは、次の子デバイスのハードウェア Id を作成します。

Stream\\MyCrossbar\#PCI\#VEN\_XXXX & DEV\_YYYY & SUBSYS\_ZZZZZZZZ & REV\_VV

Stream\\MyCrossbar\#PCI\#VEN\_XXXX & DEV\_YYYY & SUBSYS\_ZZZZZZZZ

Stream クラスは、親デバイスによって報告された互換性のある id と同じプロセスを使用します。 Stream クラスは、フォームの子デバイスの互換性のある ID を作成します。

Stream\\*&lt;pnpid&gt;*\#*&lt;親互換性 ID の変更&gt;*

互換性のある id 名の変更と長さの規則は、ハードウェア Id に対してと同じです。

たとえば、親デバイスが記述されている場合は以前、次の互換性のある Id を報告します。

PCI\\VEN\_XXXX &AMP; DEV\_YYYY &AMP; REV\_VV

PCI\\VEN\_XXXX &AMP; DEV\_YYYY

PCI\\VEN\_XXXX &AMP; CC\_ZZZZZZ

PCI\\VEN\_XXXX &AMP; CC\_ZZZZ

PCI\\VEN\_XXXX

PCI\\CC\_ZZZZZZ

PCI\\CC\_ZZZZ

**MyCrossbar**子デバイスを次の互換性のある Id ストリーム クラスを報告します。

Stream\\MyCrossbar\#PCI\#VEN\_XXXX & DEV\_YYYY & REV\_VV

Stream\\MyCrossbar\#PCI\#VEN\_XXXX & DEV\_YYYY

Stream\\MyCrossbar\#PCI\#VEN\_XXXX & CC\_ZZZZZZ

Stream\\MyCrossbar\#PCI\#VEN\_XXXX & CC\_ZZZZ

Stream\\MyCrossbar\#PCI\#VEN\_XXXX

Stream\\MyCrossbar\#PCI\#CC\_ZZZZZZ

Stream\\MyCrossbar\#PCI\#CC\_ZZZZ

Stream\\MyCrossbar

**注**   DirectX 9.0 以降、従来のハードウェア ID、Stream で\\*&lt;pnpid&gt;* が最も低い順位互換性 ID として引き続きレポートされます。 その結果、従来のドライバーは、変更せずにこれらのプラットフォームで機能を続行します。
ただし、DirectX 9.0 のリリース時点で Microsoft をお勧めするベンダーの書き込み*ストリーム クラスのバスの列挙子を利用する新規または変更されたドライバーは新しいハードウェア ID の形式を使用して*します。 ドライバーは、INF ファイルで互換性のある Id の一覧で、古い ID を含めることによって、ストリーム クラスの以前のバージョンを実行しているプラットフォームをサポートできます。

 

 

 




