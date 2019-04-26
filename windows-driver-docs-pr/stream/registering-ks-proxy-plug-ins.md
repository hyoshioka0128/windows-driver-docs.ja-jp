---
title: KS プロキシ プラグインの登録
description: KS プロキシ プラグインの登録
ms.assetid: 1f8691cb-5371-4039-a081-7c422dcac5a8
keywords:
- カーネル ストリーミング プロキシ WDK AVStream、プラグインを登録します。
- プラグインを WDK AVStream のカーネル ストリーミング プロキシの登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 199aa3085576dbf2242d7cd30bc503b0e7e4753d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358983"
---
# <a name="registering-ks-proxy-plug-ins"></a>KS プロキシ プラグインの登録


インターフェイスとプロパティの両方のページ プラグインは、KS プロキシの拡張機能のプロバイダーとして、KS プロキシを登録する必要があります。

呼び出された関数のエクスポート プラグインを登録する[DllRegisterServer](https://go.microsoft.com/fwlink/p/?linkid=106441)と[DllUnregisterServer](https://go.microsoft.com/fwlink/p/?linkid=106443)で COM オブジェクトを実装する DLL です。 これらの関数が宣言されている*Olectl.h*はユーザー定義しますが、します。

コンポーネントの CLSID、コンポーネントをサポートするインターフェイスの IID とプロパティ セットの GUID を再利用できます。

実装**DllRegisterServer**次を実行する必要があります。

1.  呼び出す[AMovieDllRegisterServer2](https://go.microsoft.com/fwlink/p/?linkid=106448)の値を持つ**TRUE**フィルターを登録します。

2.  呼び出す[RegCreateKeyEx](https://go.microsoft.com/fwlink/p/?linkid=106454)を作成し、HKLM を識別するハンドルを受信\\システム\\CurrentControlSet\\コントロール\\MediaInterfaces キー。

3.  使用[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=106447) HKLM 下の値を設定する\\システム\\CurrentControlSet\\コントロール\\MediaInterfaces キー、プロパティをマップする、インターフェイスのハンドラーに設定します。 インターフェイスのハンドラーの詳細については、次を参照してください。[インターフェイス ハンドラー プラグイン](interface-handler-plug-in.md)します。

4.  キーは、定義済みのレジストリ キーのいずれかではありません、ために、呼び出す[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=106444)キーを識別するハンドルを閉じます。

5.  呼び出す**RegCreateKeyEx**します。

6.  使用**RegSetValueEx** HKLM 下の値を設定する\\システム\\CurrentControlSet\\コントロール\\MediaSets\\プロパティ ページに、プロパティをマップするキーを設定します。 プロパティ ページのプラグインの詳細については、次を参照してください。[プロパティ ページのプラグイン](property-page-plug-in.md)します。

7.  キーは、定義済みのレジストリ キーのいずれかではありません、ために、呼び出す**RegCloseKey**キーを識別するハンドルを閉じます。

実装**DllUnregisterServer**次を実行する必要があります。

1.  呼び出す**AMovieDllRegisterServer2**の値を持つ**FALSE**フィルターの登録を解除します。

2.  呼び出す**RegCreateKeyEx**を既存のキーを開きます。

3.  使用[RegDeleteKey](https://go.microsoft.com/fwlink/p/?linkid=106446)サブキーを削除します。

4.  呼び出す**RegCloseKey**キーを識別するハンドルを閉じます。

 

 




