---
title: デバイス情報セット
description: デバイス情報セット
ms.assetid: 20539c63-10b1-408a-8c60-da444f54b64e
keywords:
- デバイス情報要素 WDK デバイスのインストール
- デバイス情報設定の WDK デバイスのインストール
- 情報は、WDK のデバイスを設定します。
- WDK のデバイス情報を列挙します。
- SetupDiEnumDeviceInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3cb7c60cea5fa761d67f1ee3693b275e661f121
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357804"
---
# <a name="device-information-sets"></a>デバイス情報セット





ユーザー モードでは、いずれかに属しているデバイスで[デバイス セットアップ クラス](device-setup-classes.md)または[デバイス インターフェイス クラス](device-interface-classes.md)を使用して管理されて*デバイス情報要素*と*デバイス情報のセット。* デバイス情報のセットは、一部のデバイス セットアップ クラスまたはインターフェイス クラスのデバイスに属しているすべてのデバイスのデバイス情報の要素で構成されます。

デバイス情報の各要素には、デバイスへのハンドルが含まれています。 *devnode*、し、その要素で記述されるデバイスに関連付けられているすべてのデバイス インターフェイスのリンク リストへのポインター。 デバイス情報のセットには、セットアップ クラスのメンバーについて説明します、要素がありますを指していない場合、デバイス インターフェイス セットアップ クラスのメンバーがインターフェイスに必ずしも関連付けられていないためです。

次の図は、デバイス情報のセットの内部構造を示します。

![デバイス情報のセットを示す図](images/devinfosets.png)

### <a name="creating-a-device-information-set"></a>デバイス情報のセットを作成します。

デバイス情報の作成と設定後[ **SetupDiCreateDeviceInfoList**](https://msdn.microsoft.com/library/windows/hardware/ff550956)、デバイス情報の要素を作成して使用して一度に 1 つ一覧に追加できる[ **SetupDiCreateDeviceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff550952)します。 または、 [ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)デバイス情報が指定されたデバイス セットアップ クラスまたはインターフェイス クラスのデバイスに関連付けられたすべてのデバイスの構成設定を作成するということができます。

### <a name="enumerating-device-information"></a>デバイスの情報を列挙します。

デバイス情報のセットが作成されると、デバイスと、セットに属するデバイス インターフェイスの両方を列挙することができますが、さまざまな操作は、列挙体の各型に必要な。 [**SetupDiEnumDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff551010)すべてのデバイス情報のセットに属する特定の条件を満たすを列挙します。 呼び出しごとに**SetupDiEnumDeviceInfo**抽出、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)デバイス情報の要素にほぼ対応する構造体。 SP_DEVINFO_DATA には、デバイスが属するクラスの GUID が含まれています、*デバイス インスタンス*デバイス devnode を指すハンドル。 SP_DEVINFO_DATA 構造体と完全なデバイス要素の主な相違点は、SP_DEVINFO_DATA は*いない*デバイスに関連付けられているインターフェイスのリンク リストを含めることが。 そのため、 **SetupDiEnumDeviceInfo**デバイス情報のセットにインターフェイスを列挙するために使用できません。

デバイス情報のセット内のデバイスのインターフェイスを列挙するために呼び出す[ **SetupDiEnumDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff551015)します。 デバイス情報ですべてのデバイス情報の要素をこの日常的な手順は、設定、各要素のインターフェイスの一覧で示されるインターフェイスを抽出し、呼び出しごとに 1 つのインターフェイスを返します。 場合**SetupDiEnumDeviceInterfaces** SP_DEVINFO_DATA 構造体が渡される 2 番目のパラメーターの入力として制約 SP_DEVINFO_DATA で指定されたデバイスに関連付けられているインターフェイスだけを列挙します。

**SetupDiEnumDeviceInterfaces**を返します、 [ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)構造体。 SP_DEVICE_INTERFACE_DATA には、インターフェイス クラス GUID とインターフェイスの名前を取得するために使用できる情報はエンコード予約済みのフィールドを含め、インターフェイスの詳細については、その他の情報が含まれています。 インターフェイス名を取得するには、さらに 1 つの手順が必要です。[**SetupDiGetDeviceInterfaceDetail** ](https://msdn.microsoft.com/library/windows/hardware/ff551120)呼び出す必要があります。 **SetupDiGetDeviceInterfaceDetail**型の構造体を返す[ **SP_DEVICE_INTERFACE_DETAIL_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552343)インターフェイスを定義するシステム オブジェクトのツリー内のパスを格納しています。

 

 





