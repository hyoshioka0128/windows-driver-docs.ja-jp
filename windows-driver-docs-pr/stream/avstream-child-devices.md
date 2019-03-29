---
title: AVStream の子デバイス
description: AVStream の子デバイス
ms.assetid: 4b2528d7-acc7-40eb-a351-64d8564c7a13
keywords:
- WDK AVStream の子デバイス
- AVStream 子デバイス WDK
- バスの WDK AVStream 列挙型
- ハードウェア Id の WDK AVStream
- WDK AVStream の識別子
- 互換性のある Id WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90e2811f7ce6aceafd4a4e94893f1623c2afd3b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571176"
---
# <a name="avstream-child-devices"></a>AVStream の子デバイス





このセクションでは、そのプラットフォームに DirectX 9.0 以降がインストールされている場合にのみ、Microsoft Windows Server 2003 と以前のオペレーティング システムに適用されます。

AVStream は子デバイス内の各キーを作成する、デバイスのバスのエミュレーターを果たすことができます、 **Enum**分岐します。 これを行うには、配置、 **Enum**デバイス キーの下のレジストリ内のブランチです。

具体的には、 **AddReg**ドライバーの INF ファイル、仕入先のセクションは、値を提供*pnpid*型 REG の\_にある各エントリの SZ**列挙型**。 AVStream を使用してこの文字列値、プラグ アンド プレイ (PnP) を構築するハードウェア ID 個々 の子デバイスごとにします。

リリースで DirectX 9.0 より前 AVStream 子デバイス ハードウェアの ID を作成、フォームの"AVStream\\*&lt;pnpid&gt;*"(場所&lt;pnpid&gt; の値です*pnpid*特定のデバイス)。

たとえば、仕入先がでは、次を指定します、 **AddReg** INF ファイルのセクション。

```INF
[MyTVDevice.AddReg]
HKR,"ENUM\CrossbarDevice",pnpid,,"MyCrossbar"
HKR,"ENUM\TunerDevice",pnpid,,"MyTuner"
```

したがって、AVStream では、次のデバイス Id で 2 つの子デバイスを作成します。

AVStream\\MyCrossbar

AVStream\\MyTuner

同じを指定する 2 つの異なる子デバイスからであいまいさを解決するのには*pnpid*値、DirectX 9.0 と報告の各子デバイス Id を後で変更します。 親デバイスによって報告されたハードウェア id ごとに、AVStream は、次の形式で子デバイスの ID を作成します。

AVStream\\*&lt;pnpid&gt;*\#*&lt;親ハードウェア ID の変更&gt;*

変更された親のハードウェア ID は、各円記号と、親のハードウェア ID (**\\**) 文字に置き換え、番号記号 (**\#**)。

AVStream を結果の文字列が長すぎる場合、最大で ID 文字列を終了します\_デバイス\_ID\_LEN 文字を含む、 **NULL**ターミネータです。 Windows Server 2003 では、この制限は 200 文字で設定*cfgmgr32.h*します。

たとえば、親デバイスは、次のハードウェア Id を報告します。

PCI\\VEN\_XXXX &AMP; DEV\_YYYY &AMP; SUBSYS\_ZZZZZZZZ &AMP; REV\_VV

PCI\\VEN\_XXXX &AMP; DEV\_YYYY &AMP; SUBSYS\_ZZZZZZZZ

使用したデバイスの*pnpid*のキー **MyCrossbar**AVStream は、次の子デバイスのハードウェア Id を作成します。

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX & DEV\_YYYY & SUBSYS\_ZZZZZZZZ & REV\_VV

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX & DEV\_YYYY & SUBSYS\_ZZZZZZZZ

AVStream は、親デバイスによって報告された互換性 Id を同じプロセスを使用します。 AVStream は、フォームの子デバイスの互換性のある ID を作成します。

AVStream\\*&lt;pnpid&gt;*\#*&lt;親互換性 ID の変更&gt;*

互換性のある id 名の変更と長さの規則は、ハードウェア Id に対してと同じです。

たとえば、親デバイスが既に記述されている場合は、次の互換性のある Id を報告します。

PCI\\VEN\_XXXX &AMP; DEV\_YYYY &AMP; REV\_VV

PCI\\VEN\_XXXX &AMP; DEV\_YYYY

PCI\\VEN\_XXXX &AMP; CC\_ZZZZZZ

PCI\\VEN\_XXXX &AMP; CC\_ZZZZ

PCI\\VEN\_XXXX

PCI\\CC\_ZZZZZZ

PCI\\CC\_ZZZZ

**MyCrossbar**子デバイスを次の互換性のある Id AVStream を報告します。

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX & DEV\_YYYY & REV\_VV

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX & DEV\_YYYY

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX & CC\_ZZZZZZ

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX & CC\_ZZZZ

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX

AVStream\\MyCrossbar\#PCI\#CC\_ZZZZZZ

AVStream\\MyCrossbar\#PCI\#CC\_ZZZZ

AVStream\\MyCrossbar

**注**   DirectX 9.0 以降、従来のハードウェア ID、AVStream で\\*&lt;pnpid&gt;* が最も低い順位互換性 ID として引き続きレポートされます。 その結果、従来のドライバーは、変更せずにこれらのプラットフォームで機能を続行します。
ただし、DirectX 9.0 のリリース時点で勧め AVStream クラス bus 列挙子を利用する新規または変更されたドライバーを記述するベンダーが新しいハードウェア ID の形式を使用します。 ドライバーは、INF ファイルで互換性のある Id の一覧で、古い ID を含めることによって AVStream の以前のバージョンを実行するプラットフォームをサポートできます。

 

 

 




