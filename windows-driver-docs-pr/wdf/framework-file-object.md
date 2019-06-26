---
title: フレームワーク ファイル オブジェクト
description: フレームワーク ファイル オブジェクト
ms.assetid: dd8215ee-2c10-4e49-9d7f-d2295bf219da
keywords:
- UMDF オブジェクト WDK、ファイル オブジェクト
- フレームワークは、WDK UMDF、ファイル オブジェクトをオブジェクトします。
- ファイル オブジェクト WDK UMDF
- IWDFFile
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5ef2dd3ebfbc7bee94ff6d9d40c368ca6c12e66
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368658"
---
# <a name="framework-file-object"></a>フレームワーク ファイル オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーにフレームワーク ファイルのオブジェクトが公開されている、 [IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)インターフェイス。 開いているデバイスのフレームワークの表現になります。 アプリケーションが Microsoft Win32 を使用してデバイスを開くと[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数の場合、フレームワークが開かれているデバイスのインスタンスを表すファイル オブジェクトを作成します。 そのため、フレームワーク ファイルのオブジェクトは、アプリケーションの呼び出しから返される Win32 ハンドルと概念的に同じ**CreateFile**します。 フレームワークには、1 つのデバイスに関連付けられている複数のファイル オブジェクトを作成できます。 成功した呼び出しごとに各ファイル オブジェクトが作成された**CreateFile**します。 特定のファイル オブジェクトのインスタンスには、読み取りと書き込みのように、すべての I/O 操作が対象とします。

**注**   UMDF ドライバーに渡されるすべての要求がファイルのオブジェクトに関連付けられています。 ただし、要求に渡される[WDM](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)と[KMDF](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)ドライバーがないファイルのオブジェクトに関連付けられて場合があります。

 

UMDF ドライバーを呼び出すことができます、 [ **IWDFIoRequest::GetFileObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getfileobject)メソッド、要求に関連付けられたファイル オブジェクトを取得します。

ドライバーを呼び出すと[ **GetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getfileobject)フレームワークは、インターフェイスの参照カウントをインクリメントします。 ドライバーはインターフェイス ポインターの使用が終わったら、参照を解放します。 スマート ポインターを自動的に使用するか、そのためには、参照カウントをデクリメント コンテキスト、または呼び出しから出たとき[**リリース**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)を使い終わったら、インターフェイスにします。 スマート ポインターを使用する方法を示すコード例を参照してください。 **GetFileObject**します。

 

 





