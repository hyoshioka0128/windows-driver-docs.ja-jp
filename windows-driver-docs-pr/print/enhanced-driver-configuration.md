---
title: 拡張ドライバー構成
description: V4 印刷ドライバーの拡張ドライバーの構成情報を提供する GPD と PPD ファイルを使用できます。
ms.assetid: B208C661-4D5B-467A-8451-4382453EC09A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: faafea3dfbe1dbe85258807e26345432e3105b3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581424"
---
# <a name="enhanced-driver-configuration"></a>拡張ドライバー構成


V4 印刷ドライバーの拡張ドライバーの構成情報を提供する GPD と PPD ファイルを使用できます。

V4 ドライバー モデルに基づく印刷ドライバーは、双方向を使用してデバイスからこれらの GPD と PPD ファイルを取得できます。 これにより、印刷クラス ドライバーを使用して、Windows Update から追加のダウンロードを必要とせずより豊富な機能をサポートするデバイスです。

この機能は Ws-print v1.1 をサポートするドライバーに対して既定でサポートされています。 ただし、TCP/IP デバイスおよび Ws-print v1.0 デバイス可能性がありますもこの機能をサポート、次の Bidi スキーマ要素を指定する双方向の拡張機能のファイルを実装することで。

**スキーマのパス: GPD/PPD ファイルの読み取りにスキーマ セクション**

**セクション名:** DriverConfigFiles

**スキーマのパス:**\\Printer.Configuration.DriverConfigFiles

**説明 :** Bidi スキーマは、この新しいセクションでは、ドライバーの構成データ、GPD PPD 説明ファイルなどのデバイスを照会するスキーマの値が格納されます。

GPD ファイルを読み取るための拡張機能

**スキーマ名:** GPDFile

**スキーマのパス:**\\Printer.Configuration.DriverConfigFiles:GPDFile

**ノードの種類:**[値]

**データの種類:** BIDI\_文字列

**説明 :** デバイスの完全な GPD ファイルです。 これには、使用可能で、デバイスの現在の設定に従って最新の状態は、すべての特定のデバイス構成情報が含まれています。

PPD ファイルを読み取るための拡張機能

**スキーマ名:** PPDFile

**スキーマのパス:**\\Printer.Configuration.DriverConfigFiles:PPDFile

**ノードの種類:**[値]

**データの種類:** BIDI\_文字列

**説明 :** デバイスの完全な PPD ファイルです。 これには、使用可能で、デバイスの現在の設定に従って最新の状態は、すべての特定のデバイス構成情報が含まれています。

**注**  、USB デバイスの GPD や PPD ファイルを使用しているかどうか双方向の拡張 XML ファイルする必要があります drvPrinterEvent 属性を指定し、"true"には、その値を設定します。 これにより、双方向のキャッシュが更新された後、要素が更新されます。

 

次の XML フラグメントでは、drvPrinterEvent 属性を使用するための正しい構文を示しています。

```xml
<?xml version='1.0'?>
...
  <Property name='DeviceInfo'>
     <Const name="Category" type="BIDI_STRING" value="DeviceCategory"/> 
     <Value name="QueueProperty" type="BIDI_STRING" accessType="Get" queryKey="Configuration" refreshInterval="60" drvPrinterEvent="true"/> 
  </Property> 
...
```

## <a name="related-topics"></a>関連トピック

[V4 プリンター ドライバーの接続](v4-printer-driver-connectivity.md)  



