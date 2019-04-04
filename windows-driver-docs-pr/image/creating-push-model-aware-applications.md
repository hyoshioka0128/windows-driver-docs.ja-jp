---
title: プッシュ モデル対応のアプリケーションを作成します。
description: プッシュ モデル対応のアプリケーションを作成します。
ms.assetid: 0f554b2c-0217-4109-8ef6-99c5400dfed6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f80031cc9d7a1f132dbdcd854dedfe30e142a43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549232"
---
# <a name="creating-push-model-aware-applications"></a>プッシュ モデル対応のアプリケーションを作成します。





プッシュ モデル対応のアプリケーションとは、登録されている Microsoft STI にも自動的にアクティブにできます静止画像デバイス イベントが発生したときにようにです。 アプリケーションにプッシュ モデルを可能では、次の 2 つのメソッドのいずれかに注意してください。

-   呼び出す[ **IStillImage::RegisterLaunchApplication**](https://msdn.microsoft.com/library/windows/hardware/ff543798)します。 呼び出しは、アプリケーションまたはそのインストール プログラムが可能です。

-   アプリケーションのセットアップ情報 (INF) ファイルにエントリを含むです。 エントリを参照する必要があります、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320) INF ファイルにします。 エントリの構文は次の例に示します。

    ```INF
    ; Register Application "Imaging" as a push-model aware application for use with the still image event monitor
    HKLM,"SOFTWARE\Microsoft\Windows\CurrentVersion\StillImage\Registered Applications",Imaging,,"%25%\KodakImg.Exe /StiDevice:%%1 /StiEvent:%%2"
    ```

    2 つの INF ファイルのエントリは、プッシュ モデル対応のアプリケーションをサポートするデバイスの必要があります。**DeviceData**と**イベント**します。 詳細については、[静止画像デバイスの INF ファイル](inf-files-for-still-image-devices.md)を参照してください。

これらのメソッドのいずれかの原因に登録するアプリケーション、[イメージ イベント モニターではまだ](overview-of-sti-components.md#ddk-still-image-event-monitor-si)します。

プッシュ モデルの対応として、アプリケーションが登録されると、ユーザーを割り当てることが[イメージ デバイス イベントではまだ](still-image-device-events.md)スキャナーとカメラのコントロール パネルでアプリケーションにします。 さらに、ベンダーは、デバイス ドライバーの INF ファイル内のアプリケーション名を含めることによってアプリケーションにデバイス イベントの最初の割り当てを提供できます。 ユーザーは、スキャナーとカメラのコントロール パネルでこの初期の割り当てを変更できます。

デバイス イベントは、アプリケーションに割り当てられている、後に割り当てられたデバイス イベントの発生を検出した場合にイベント モニターはアプリケーションを起動します。

呼び出して、プッシュ モデル対応のアプリケーションがアクティブになる[ **IStillImage::GetSTILaunchInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff543790)イベントと起動されたデバイスを決定します。 呼び出して[ **IStillImage::GetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff543782)デバイスに関する詳細情報を取得します。

アプリケーションは、イベントを処理する必要があります。 またはイベントを処理できない理由を説明するユーザーの表示を作成する必要があります。 多くの場合、ユーザーは使用してコントロール パネルにデバイス イベントを他のアプリケーションに関連付けます。

通常、イベントを処理、イメージの閲覧を意味します。 これを行うには、アプリケーションが通常は呼び出して、 [Image Acquisition API](overview-of-sti-components.md#ddk-image-acquisition-api-si)、TWAIN など。

イベントが発生しましたが、イメージの取得 API がデータ モードでにデバイスが開かれていないため、アプリケーションが開始された場合 (を参照してください[転送モード](transfer-modes.md))、別のイベントが場合、イベント モニターのアプリケーションの別のインスタンスが起動します。検出されました。 により、複数のインスタンスまたは (可能であれば) が認識するため、最初のインスタンスではありません、イベントを識別する最初のインスタンスにメッセージを送信して終了しますように、アプリケーションを実装する必要があります。

 

 




