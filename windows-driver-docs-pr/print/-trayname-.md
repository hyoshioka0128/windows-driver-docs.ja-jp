---
title: '\ TrayName\ (InputBins)'
description: '\ TrayName\ (InputBins)'
ms.assetid: 7fa03413-5b95-443f-9b0f-75d82d0e41cf
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e670d7a572555493412f1a6cf86775170750871
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372856"
---
# <a name="trayname-inputbins"></a>\[TrayName\] (InputBins)


スキーマのパス:\\Printer.Layout.InputBins\[ 。TrayName\]

ノード型: プロパティ

説明: 入力のトレイに、IHV マップのプロパティ名。 IHV は、次の一覧から名前で入力ビンの IHV 固有トレイ名にマップできます。

トレイ 1

トレイ 2

Trayxx (xx 任意の正の整数)

TopBin

MiddleBin

BottomBin

LargeCapacityBin

ManualBin

EnvelopeBin

EnvelopeManual

MultiPurposeBin

\[TrayName\]プロパティには、次の子の値が含まれています。

インストール済み

MediaSize

MediaColor

容量

Level

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> インストールされています。

スキーマのパス:\\Printer.Layout.InputBins\[ 。TrayName\]: インストールされています。

ノード型: 値

データ型: BIDI\_BOOL

説明: ビンがによって参照されるかどうかを示す\[TrayName\]デバイスにインストールされます。 場合**TRUE**、デバイスで、箱がインストールされている場合は**FALSE**ビンがデバイスにインストールされていません。

### <a name="span-idmediasizespanspan-idmediasizespan-mediasize"></a><span id="mediasize"></span><span id="MEDIASIZE"></span> MediaSize

スキーマのパス:\\Printer.Layout.InputBins\[ 。TrayName\]: MediaSize

ノード型: 値

データ型: BIDI\_文字列

説明: 現在参照されている入力ビンで使用可能なメディアのサイズ。 値は、IEEE は PWG 標準 5101.1 2001-メディア名を標準化に従う必要があります。
次の値が許可されている: na\_法的\_8.5x14in

na\_文字\_8.5x11in

iso\_a4\_210x297mm

iso\_c5\_162x229mm

iso\_dl\_110x220mm

jis\_b4\_257x364mm

### <a name="span-idmediatypespanspan-idmediatypespan-mediatype"></a><span id="mediatype"></span><span id="MEDIATYPE"></span> メディアの種類

スキーマのパス:\\Printer.Layout.InputBins\[ 。TrayName\]: メディアの種類

ノード型: 値

データ型: BIDI\_文字列

説明: 現在参照されている入力ビンで使用可能なメディアの種類。 値は、IEEE は PWG 標準 5101.1 2001-メディア名を標準化に従う必要があります。
次の値が許可されている: 厚紙

エンベロープ

labels

写真

ひな形

ひな形のインク ジェット

透過性

その他

### <a name="span-idmediacolorspanspan-idmediacolorspan-mediacolor"></a><span id="mediacolor"></span><span id="MEDIACOLOR"></span> MediaColor

スキーマのパス:\\Printer.Layout.InputBins\[ 。TrayName\]: MediaColor

ノード型: 値

データ型: BIDI\_文字列

説明: 現在参照されている入力ビンで使用可能なメディアの色。 値は、IEEE は PWG 標準 5101.1 2001-メディア名を標準化に従う必要があります。
次の値が許可されている: 白

ピンク

黄色

buff

ゴールデンロッド

青

緑色

赤色

灰色

象牙

オレンジ色

色のなし

unknown

### <a name="span-idfeeddirectionspanspan-idfeeddirectionspan-feeddirection"></a><span id="feeddirection"></span><span id="FEEDDIRECTION"></span> FeedDirection

スキーマのパス:\\Printer.Layout.InputBins\[ 。TrayName\]: FeedDirection

ノード型: 値

データ型: BIDI\_文字列

説明: 現在参照されている入力ビンで最初のメディア パスを入力し、値は次のいずれかを指定する必要があります、用紙の端を示します。

LongEdgeFirst

ShortEdgeFirst

### <a name="span-idcapacityspanspan-idcapacityspan-capacity"></a><span id="capacity"></span><span id="CAPACITY"></span> 容量

スキーマのパス:\\Printer.Layout.InputBins\[ 。TrayName\]: 容量

ノード型: 値

データ型: BIDI\_INT

説明: 現在参照されている入力ビンのシートで、容量。

### <a name="span-idlevelspanspan-idlevelspan-level"></a><span id="level"></span><span id="LEVEL"></span> レベル

スキーマのパス:\\Printer.Layout.InputBins\[ 。TrayName\]: レベル

ノード型: 値

データ型: BIDI\_INT

説明: に対する割合で表した、現在参照されている入力ビンに残っている容量です。 完全なトレイは、空のトレイ値が 0 のときに、100 の値になります。 レベルが測定可能でない場合は-1 (不明なレベルを示す) の値が返されます。

 

 




