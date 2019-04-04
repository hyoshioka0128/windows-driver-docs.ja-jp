---
title: ISensorClassExtension について
description: ISensorClassExtension について
ms.assetid: 1f55f28a-796a-40e5-9995-e6a28761b9a4
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7af3c76e885cb050b4751f598fbe02ed7673105b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572664"
---
# <a name="about-isensorclassextension"></a>ISensorClassExtension について


センサー ドライバーでは、ISensorClassExtension を使用して、初期化、センサー クラスの拡張機能の初期化を解除し、イベントを発生させる、プロセス WPD 入力/出力の制御 (Ioctl) コードと正しく UMDF ファイル ハンドルを閉じます。

## <a name="methods-to-manage-object-lifetime"></a>オブジェクトの有効期間を管理する方法

PnP ベースのハードウェア センサー ドライバーを呼び出し、クラス拡張を初期化する[ **ISensorClassExtension::Initialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-initialize)で UMDF によって呼び出されたとき[ **IPnpCallbackHardware::OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)します。 この手順では、ドライバーの主なクラスとクラスの拡張機能オブジェクトによって発生するイベントを処理するコールバック インターフェイスを実装するクラスにポインターをクラスの拡張機能オブジェクトを提供します。 UMDF によってドライバーが呼び出されたとき[ **IPnpCallbackHardware::OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)を呼び出す必要が[ **ISensorClassExtension::Uninitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-uninitialize)クラスの拡張機能オブジェクトを離します。 一部の種類のセンサーをさまざまなタイミングで、クラス拡張を初期化してに必要があることに注意してください。

## <a name="methods-to-raise-events"></a>イベントを発生させるメソッド

ドライバーはさまざまな種類のセンサー イベントを発生させることができます (センサー データを含んでいる通常) を呼び出して[ **ISensorClassExtension::PostEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)と呼び出すことによって状態情報イベント[ **ISensorClassExtension::PostStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)します。 センサー ドライバーでイベントを使用する方法についての詳細については、[センサー ドライバー イベントについて](about-sensor-driver-events.md)を参照してください。

## <a name="methods-to-manage-ioctls-and-handles"></a>Ioctl とハンドルを管理する方法

センサー ドライバーには、クラス拡張の UMDF 呼び出しの 2 種類が転送先します。

-   I/O を処理する要求で受信したコードを制御する[ **IQueueCallbackDeviceIoControl::OnDeviceIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)します。 クラスの拡張を処理するために、I/O 要求を転送するように、ドライバーを呼び出す必要があります[ **ISensorClassExtension::ProcessIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-processiocontrol)します。

-   クライアントの終了に関する通知ファイルで受信したハンドル[ **IFileCallbackCleanup::OnCleanupFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)します。 I/O 要求のキャンセルを転送するように、ドライバーを呼び出す必要があります[ **ISensorClassExtension::CleanupFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-cleanupfile)します。

 

 




