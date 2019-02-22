---
title: RAW 形式のデータ転送
description: RAW 形式のデータ転送
ms.assetid: 8541b5ce-fd55-47b0-9687-162fb2b4e6aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2066fca36d6ab0d4306a246858186c8d8cdcc99f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560667"
---
# <a name="raw-format-data-transfer"></a>RAW 形式のデータ転送

WIA では、データ転送の生の形式をサポートします。 WIA 転送の RAW 形式の利点は、スキャン頭の中のすべての機能をサポートしています。

[ **WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)プロパティは、未加工の形式の GUID のシンボリック名に設定することができます**WiaImgFmt\_RAW**します。

RAW 形式のデータ転送のサポートを追加するには、スキャナーのドライバーはすべて、標準のことが必要[WIA スキャナー プロパティ](properties-for-wia-scanner-minidrivers.md)します。 標準的なスキャナーのプロパティには、画像エクステント、解決、および 1 ピクセルあたりのチャネルのものが含まれます。 ドライバーでのチャネルあたりのビット数も指定する必要があります、 [ **WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff551641)プロパティ。

生の形式は*いない*するためのものファイル形式でなければなりません。 データ転送の一部のみになります。 イメージング アプリケーションは、標準のイメージ ファイル形式の生データを変換します。 [ **WIA\_IPA\_FILENAME\_拡張子**](https://msdn.microsoft.com/library/windows/hardware/ff551549)プロパティは空の文字列に設定する必要があります (意味""なく**NULL**、として**NULL**一部のアプリケーションの問題になることができます)。

DWORD 揃えスキャン ラインがあります。 スキャン ラインには、その長さが 4 バイトの倍数をあるように、最後に埋め込まれている必要があります。 各スキャン ライン内のピクセルをパックする必要があります。 イメージ データを圧縮または圧縮されていないことができます。

**注**  圧縮されていないイメージ データは、データがパックされたピクセル形式である必要があります。 ミニ-ドライバーをアンパック ピクセル形式にによって平面のスキャンを変換する必要があります。

ここでは、次のトピックに関する追加情報を示します。

[WIA 生データのヘッダー](wia-raw-data-header.md)

[RAW 形式転送プロパティの検証](property-validation-for-raw-format-transfers.md)
