---
title: センサー クラスの拡張機能にアクセスします。
description: センサー クラスの拡張機能にアクセスします。
ms.assetid: 206A00AE-45D7-49D8-97E2-45A6DACFCB08
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0b1325be764d4272929c2802a6a705b45921d3b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376432"
---
# <a name="access-the-sensor-class-extension"></a>センサー クラスの拡張機能にアクセスします。


| モジュール     | クラス/インターフェイス |
|------------|-----------------|
| Device.cpp | CMyDevice       |

 

Microsoft では、2 つのセンサー Api をサポートします。 両方にアクセスするデバイス、データの取得とプロパティの設定を簡略化します。

-   **デスクトップ API** (従来のデスクトップ アプリ) - COM/Win32; を使用して C++ でアプリを作成します。
-   **WinRT API** (Windows アプリ) の HtML と JavaScript、または、XAML および Visual Basic の場合でアプリを記述するC#または C++ です。

センサー クラスの拡張機能 (**ISensorClassExtension**) には、センサー ドライバーとセンサーの Api をリンクします。 ドライバーは、次の作業を使用します。

-   初期化し、センサー クラスの拡張を初期化解除
-   イベントを発生させる
-   プロセス WPD 入力/出力制御コード (Ioctl)
-   UMDF ファイル ハンドルを閉じる

## <a name="initializing-the-class-extension"></a>クラスの拡張機能の初期化

SpbAccelerometer サンプル WUDFx.dll (Windows のユーザー モード ドライバー フレームワークのコンポーネント) を呼び出すときに、クラス拡張を初期化します**CMyDevice::OnPrepareHardware**:

```cpp
if (SUCCEEDED(hr))
{
    // Initialize the sensor class extension
    hr = m_spClassExtension->Initialize(pWdfDevice, spUnknown);
}
```

### <a name="releasing-the-class-extension"></a>クラスの拡張機能をリリース

サンプル ドライバーの初期化を解除し、CMyDevice::OnReleaseHardware が呼び出されたときに、クラス拡張を解放します。

```cpp
if (m_spClassExtension != nullptr)
{
   hr = m_spClassExtension->Uninitialize();
}
```

### <a name="supporting-data-events-with-the-class-extension"></a>クラスの拡張機能に対応するデータ イベント

センサー アプリのデータ イベントのイベント ハンドラーを登録する場合、ドライバーのサンプルの投稿を使用してイベント通知**ISensorClassExtension::PostEvent**します。 内でこれが発生した**CSensorDdi::PostDataEvent**:

```cpp
if (SUCCEEDED(hr))
{
   hr = m_spClassExtension->PostEvent(SensorId, spCollection);
}
```

### <a name="supporting-state-change-events-with-the-class-extension"></a>クラスの拡張機能に対応する状態変更イベント

センサー アプリの状態変更イベントのイベント ハンドラーを登録する場合、ドライバーのサンプルの投稿を使用してイベント通知**ISensorClassExtension::PostStateChange**します。 内でこれが発生した**CSensorDdi::PostStateChange**:

```cpp
HRESULT hr = m_spClassExtension->PostStateChange(SensorId, state);
```

 

 




