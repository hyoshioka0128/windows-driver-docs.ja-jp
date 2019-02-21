---
title: フレームワークのファイル オブジェクト
description: フレームワークのファイル オブジェクト
ms.assetid: dd8215ee-2c10-4e49-9d7f-d2295bf219da
keywords:
- UMDF オブジェクト WDK、ファイル オブジェクト
- フレームワークは、WDK UMDF、ファイル オブジェクトをオブジェクトします。
- ファイル オブジェクト WDK UMDF
- IWDFFile
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3caa9e2080ec9843523ae8301ef4548c146db75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527415"
---
# <a name="framework-file-object"></a>フレームワークのファイル オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーにフレームワーク ファイルのオブジェクトが公開されている、 [IWDFFile](https://msdn.microsoft.com/library/windows/hardware/ff558912)インターフェイス。 開いているデバイスのフレームワークの表現になります。 アプリケーションが Microsoft Win32 を使用してデバイスを開くと[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)関数の場合、フレームワークが開かれているデバイスのインスタンスを表すファイル オブジェクトを作成します。 そのため、フレームワーク ファイルのオブジェクトは、アプリケーションの呼び出しから返される Win32 ハンドルと概念的に同じ**CreateFile**します。 フレームワークには、1 つのデバイスに関連付けられている複数のファイル オブジェクトを作成できます。 成功した呼び出しごとに各ファイル オブジェクトが作成された**CreateFile**します。 特定のファイル オブジェクトのインスタンスには、読み取りと書き込みのように、すべての I/O 操作が対象とします。

**注**   UMDF ドライバーに渡されるすべての要求がファイルのオブジェクトに関連付けられています。 ただし、要求に渡される[WDM](https://msdn.microsoft.com/library/windows/hardware/ff565698)と[KMDF](https://msdn.microsoft.com/library/windows/hardware/ff544296)ドライバーがないファイルのオブジェクトに関連付けられて場合があります。

 

UMDF ドライバーを呼び出すことができます、 [ **IWDFIoRequest::GetFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff559099)メソッド、要求に関連付けられたファイル オブジェクトを取得します。

ドライバーを呼び出すと[ **GetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff559099)フレームワークは、インターフェイスの参照カウントをインクリメントします。 ドライバーはインターフェイス ポインターの使用が終わったら、参照を解放します。 スマート ポインターを自動的に使用するか、そのためには、参照カウントをデクリメント コンテキスト、または呼び出しから出たとき[**リリース**](https://msdn.microsoft.com/library/windows/desktop/ms682317)を使い終わったら、インターフェイスにします。 スマート ポインターを使用する方法を示すコード例を参照してください。 **GetFileObject**します。

 

 





