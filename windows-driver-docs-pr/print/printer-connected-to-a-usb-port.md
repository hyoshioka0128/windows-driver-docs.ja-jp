---
title: USB ポートに接続されているプリンター
description: USB ポートに接続されているプリンター
ms.assetid: 85e238e1-4dc1-4720-b383-d6aaed72e560
keywords:
- WDK の USB プリンター
- バスの種類のプリンター ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 622a0d68c82afff9ec669355bc6e2015f1f17421
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579445"
---
# <a name="printer-connected-to-a-usb-port"></a>USB ポートに接続されているプリンター





USB バス ドライバーが持つ物理デバイス オブジェクト (PDO) を作成するユニバーサル シリアル バス (USB) プリンターが USB ポート経由で接続されているときに、*ハードウェア ID* VIDvvPIDpp、フォームのおよび*互換性 ID* クラス\_7。 *Devnode*列挙型の下に作成これの\\USB\\ .クラス\_7 USB ポート経由で接続されているプリンター デバイスを識別します。 プラグ アンド プレイ読み込みますクラスに互換性のある ID の一致を使用して usbprint.sys\_usbprint.inf から 7。

任意の USB プリンター デバイスの usbprint.sys を読み込むために使用 usbprint.inf からエントリは次のとおりです。

```cpp
[Microsoft]
%USBPRINT.DeviceDesc% = USBPRINT_Inst,USB\Class_07,GENERIC_USB_PRINTER
```

Usbprint.sys では、プラグ アンド プレイ プリンター 1284 の文字列を取得するクエリを実行し、並列のバスの列挙子と互換性があるハードウェア ID を生成します。 (詳細については、次を参照してください[USBPRINT インターフェイス](usb-printing.md)。)。物理デバイス オブジェクト (PDO) を持つ devnode は列挙型を作成します\\USBPRINT、形式は次の 2 つのハードウェア Id を使用して。

```cpp
USBPRINT\Company_NameModelNam1234
```

次の図には、USB ポート経由で接続されているプリンターのドライバー スタックが表示されます。

![usb プリンターのプラグ アンド プレイ](images/pnpusb01.png)

次の例では、エントリ、 [ **INF 製造元セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547454) USB またはその他のバスの種類のプリンター ドライバーをインストールに使用できます。 最初の行は、USB バスでプリンターがインストールされている場合に、ランク 0 のハードウェア ID の一致を保証します。 2 行目は、別のバス上のプリンターがインストールされている場合、ランク 0 のハードウェア ID の一致を保証します。 詳細については、[カスタムのプラグ アンド プレイ プリンター ドライバーをインストールする](installing-a-custom-plug-and-play-printer-driver.md)を参照してください。

```cpp
 "Model Name XYZ" = Install_Section_XYZ, USBPRINT\Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs  
"Model Name XYZ" = Install_Section_XYZ, Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs
```

 

 




