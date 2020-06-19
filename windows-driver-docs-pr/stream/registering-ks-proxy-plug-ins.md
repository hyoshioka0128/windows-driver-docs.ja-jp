---
title: KS プロキシ プラグインの登録
description: KS プロキシ プラグインの登録
ms.assetid: 1f8691cb-5371-4039-a081-7c422dcac5a8
keywords:
- カーネルストリーミングプロキシ WDK AVStream、プラグインの登録
- カーネルストリーミングプロキシプラグインの登録 WDK AVStream
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 25cedce82233a6c520dda1bf80d0986208f6ddb6
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073430"
---
# <a name="registering-ks-proxy-plug-ins"></a>KS プロキシプラグインを登録しています

インターフェイスとプロパティページのプラグインはどちらも、ks プロキシ拡張のプロバイダーとして KS プロキシに登録する必要があります。

プラグインを登録するには、COM オブジェクトを実装する DLL で[DllRegisterServer](https://docs.microsoft.com/windows/win32/api/olectl/nf-olectl-dllregisterserver)と[DllUnregisterServer](https://docs.microsoft.com/windows/win32/api/olectl/nf-olectl-dllunregisterserver)という名前の関数をエクスポートします。 これらの関数は*Olectl*で宣言されていますが、ユーザー定義です。

コンポーネントの CLSID およびコンポーネントがサポートするインターフェイスの IID として、プロパティセットの GUID を再利用できます。

**DllRegisterServer**の実装では、次の操作を行う必要があります。

1. フィルターを登録するには、 **TRUE**の値を指定して[AMovieDllRegisterServer2](https://docs.microsoft.com/previous-versions//ms778973(v=vs.85))を呼び出します。

1. [Regcreatekeyex](https://docs.microsoft.com/windows/win32/api/winreg/nf-winreg-regcreatekeyexa)を呼び出して、HKLM \\ System \\ CurrentControlSet \\ Control \\ mediainterfaces キーを作成し、そのハンドルを受信します。

1. [RegSetValueEx](https://docs.microsoft.com/windows/win32/api/winreg/nf-winreg-regsetvalueexa)を使用して、 \\ \\ \\ \\ プロパティセットをインターフェイスハンドラーにマップする HKLM System CurrentControlSet Control mediainterfaces キーの下に値を設定します。 インターフェイスハンドラーの詳細については、「[インターフェイスハンドラープラグイン](interface-handler-plug-in.md)」を参照してください。

1. キーが定義済みのレジストリキーの1つではないため、キーへのハンドルを閉じるには、 [Regclosekey](https://docs.microsoft.com/windows/win32/api/winreg/nf-winreg-regclosekey)を呼び出します。

1. **Regcreatekeyex**を呼び出します。

1. **RegSetValueEx**を使用して、プロパティ \\ \\ \\ \\ \\ セットをプロパティページにマップする HKLM System CurrentControlSet Control mediasets キーの下に値を設定します。 プロパティページのプラグインの詳細については、「[プロパティページプラグイン](property-page-plug-in.md)」を参照してください。

1. キーが定義済みのレジストリキーの1つではないため、キーへのハンドルを閉じるには、 **Regclosekey**を呼び出します。

**DllUnregisterServer**の実装では、次の操作を行う必要があります。

1. **FALSE**の値を指定して**AMovieDllRegisterServer2**を呼び出し、フィルターの登録を解除します。

1. **Regcreatekeyex**を呼び出して、既存のキーを開きます。

1. [Regdeletekey](https://docs.microsoft.com/windows/win32/api/winreg/nf-winreg-regdeletekeya)を使用してサブキーを削除します。

1. キーへのハンドルを閉じるには、 **Regclosekey**を呼び出します。
