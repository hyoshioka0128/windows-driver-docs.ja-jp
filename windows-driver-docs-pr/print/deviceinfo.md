---
title: DeviceInfo
description: DeviceInfo
ms.assetid: be2ee9e7-bd94-4f96-8d93-3b6f5fd9350e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 764321e1ca7b7524a6c03a66415b104f2db48a37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529851"
---
# <a name="deviceinfo"></a>DeviceInfo


スキーマのパス:\\Printer.DeviceInfo

ノード型: プロパティ

DeviceInfo プロパティには、全体として、デバイスに関する情報が含まれています。 このデータの多くは、デバイスを個人用に設定するユーザーまたは管理者によって設定できます。

DeviceInfo プロパティには、次の子の値が含まれています。

FriendlyName

製造元

ModelName

Location

Comment

FirmwareVersion

IEEE1284DeviceID

[NetworkingInfo](networkinginfo.md)

### <a name="span-idfriendlynamespanspan-idfriendlynamespan-friendlyname"></a><span id="friendlyname"></span><span id="FRIENDLYNAME"></span> FriendlyName

スキーマのパス:\\Printer.DeviceInfo:FriendlyName

ノード型: 値

データ型: BIDI\_文字列

説明: A ユーザーが作成した、ユーザーが設定可能な名前をデバイスを識別します。

### <a name="span-idmanufacturerspanspan-idmanufacturerspan-manufacturer"></a><span id="manufacturer"></span><span id="MANUFACTURER"></span> 製造元

スキーマのパス:\\Printer.DeviceInfo:Manufacturer

ノード型: 値

データ型: BIDI\_文字列

説明: デバイスの製造元の名前。

### <a name="span-idmodelnamespanspan-idmodelnamespan-modelname"></a><span id="modelname"></span><span id="MODELNAME"></span> ModelName

スキーマのパス:\\Printer.DeviceInfo:ModelName

ノード型: 値

データ型: BIDI\_文字列

説明: デバイス モデル、製造元の名前を除くモデル番号を含むの名前。

### <a name="span-idlocationspanspan-idlocationspan-location"></a><span id="location"></span><span id="LOCATION"></span> 場所

スキーマのパス:\\Printer.DeviceInfo:Location

ノード型: 値

データ型: BIDI\_文字列

説明: デバイスの現在の場所。

### <a name="span-idcommentspanspan-idcommentspan-comment"></a><span id="comment"></span><span id="COMMENT"></span> コメント

スキーマのパス:\\Printer.DeviceInfo:Comment

ノード型: 値

データ型: BIDI\_文字列

説明: A の管理者またはデバイスが存在する組織にとって重要な情報を格納している文字列。

### <a name="span-idfirmwareversionspanspan-idfirmwareversionspan-firmwareversion"></a><span id="firmwareversion"></span><span id="FIRMWAREVERSION"></span> FirmwareVersion

スキーマのパス:\\Printer.DeviceInfo:FirmwareVersion

ノード型: 値

データ型: BIDI\_文字列

デバイスの現在のファームウェア バージョンが含まれています: 説明する文字列。

### <a name="span-idieee1284deviceidspanspan-idieee1284deviceidspan-ieee1284deviceid"></a><span id="ieee1284deviceid"></span><span id="IEEE1284DEVICEID"></span> IEEE1284DeviceID

スキーマのパス:\\Printer.DeviceInfo:IEEE1284DeviceID

ノード型: 値

データ型: BIDI\_文字列

デバイスの IEEE 1284 2000 デバイス ID を含む説明: A 文字列。 [長さ] フィールドを指定しない必要がありますに注意してください。 値は、プリンタのベンダによって割り当てられるし、印刷サービスでローカライズされていない必要があります。

IEEE 1284 2000 デバイス ID は、続けて周辺機器の特性と機能を定義する ASCII 文字の大文字の文字列の長さフィールドです。 長さ (バイト) は、含めることはできません。 デバイス ID のシーケンスは、一連のキーと値の形式で構成されます。

キー: 値 {, value}、キーごとに繰り返されます。

示されるように、各キーは 1 つの値を持つし、値が 1 つ以上あります。 最低限必要なキー (大文字小文字を区別) は、製造元とモデルです。 (これらのキーがありますのように短縮製造と MDL それぞれ。)各実装は、これら 2 つのキーと可能性がある追加を指定する必要があります。 各キー (およびそれぞれの値) は、文字の文字列です。 コロン (:)、コンマ (,)、セミコロン (;) を除く任意の文字文字列のキー (または値) の一部として含めることできます。 先頭または末尾の空白 (スペース\[x '20'\]、タブ\['09' x\]、VTAB\['0B' x\]、CR\[x '0 D'\]、NL\['0A' x\]、または FF\[x '0 C'\]) 解析プログラムによって、文字列では無視されます (ただし、シーケンスの全体的な長さの一部として引き続きカウントされます)。

次のコード例は、ID 文字列を示しています。 は省略可能なコマンド セット、コメント、およびアクティブなコマンドを示していますキーと関連付けられた値に設定します。

**注**   1 行ですべてのテキストを指定する必要があります。

 

```cpp
MANUFACTURER:ACME Manufacturing;
MODEL:LaserBeam 9;
COMMAND SET:PCL,PJL,PS,XHTML-Print+xml;
COMMENT:Anything you like;
ACTIVE COMMAND SET:PCL;
```

 

 




