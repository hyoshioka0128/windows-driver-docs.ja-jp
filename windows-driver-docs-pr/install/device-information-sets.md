---
title: デバイス情報セット
description: デバイス情報セット
ms.assetid: 20539c63-10b1-408a-8c60-da444f54b64e
keywords:
- デバイス情報要素 WDK デバイスのインストール
- デバイス情報は、WDK デバイスのインストールを設定します
- 情報セット WDK デバイス
- デバイス情報の列挙 WDK
- SetupDiEnumDeviceInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff3db6aaea5612d5fc99399d3356a0813bafe2a4
ms.sourcegitcommit: 3794904c6f741bdc407dfe22341080646602f972
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "80807618"
---
# <a name="device-information-sets"></a>デバイス情報セット

ユーザーモードでは、デバイスの[セットアップクラス](device-setup-classes.md)または[デバイスインターフェイスクラス](device-interface-classes.md)に属するデバイスは、*デバイス情報要素*と*デバイス情報セット*を使用して管理されます。 デバイス情報セットは、一部のデバイスセットアップクラスまたはデバイスインターフェイスクラスに属するすべてのデバイスのデバイス情報要素で構成されます。

各デバイス情報要素には、デバイスの*devnode*へのハンドル、およびその要素によって記述されるデバイスに関連付けられているすべてのデバイスインターフェイスのリンクリストへのポインターが含まれています。 セットアップクラスのメンバーがデバイス情報セットに記述されている場合、セットアップクラスのメンバーは必ずしもインターフェイスに関連付けられていないため、要素はデバイスインターフェイスを指していない可能性があります。

次の図は、デバイス情報セットの内部構造を示しています。

![デバイス情報セットを示す図](images/devinfosets.png)

## <a name="creating-a-device-information-set"></a>デバイス情報セットを作成する

[**SetupdicreatedeviceinSetupDiCreateDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolist)を使用してデバイス情報セットを作成した後、デバイス情報要素を作成し、リストに一度に 1 [**SetupDiCreateDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)つずつ追加できます。 または、 [**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)を呼び出して、指定したデバイスセットアップクラスまたはデバイスインターフェイスクラスに関連付けられているすべてのデバイスで構成されたデバイス情報セットを作成することもできます。

## <a name="enumerating-device-information"></a>デバイス情報の列挙

デバイス情報セットを作成すると、そのセットに属するデバイスとデバイスインターフェイスの両方を列挙できますが、列挙型ごとに異なる操作が必要になります。 [**SetupDiEnumDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)は、特定の条件を満たす情報セットに属するすべてのデバイスを列挙します。 **SetupDiEnumDeviceInfo**を呼び出すたびに、デバイス情報要素にほぼ対応する[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)構造が抽出されます。 SP_DEVINFO_DATA には、デバイスが属するクラスの GUID と、デバイスの devnode を指す*デバイスインスタンス*ハンドルが含まれています。 SP_DEVINFO_DATA 構造体と完全なデバイス要素の主な違いは、SP_DEVINFO_DATA には、デバイスに関連付けられているインターフェイスのリンクリストが含まれて*いない*ことです。 そのため、 **SetupDiEnumDeviceInfo**を使用してデバイス情報セット内のインターフェイスを列挙することはできません。

デバイス情報セット内のデバイスインターフェイスを列挙するには、 [**Setupdienumdeviceinterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)を呼び出します。 このルーチンは、デバイス情報セット内のすべてのデバイス情報要素をステップ実行し、各要素のインターフェイスリスト内のインターフェイスを抽出して、呼び出しごとに1つのインターフェイスを返します。 **Setupdienumdeviceinterfaces**が2番目のパラメーターに入力として SP_DEVINFO_DATA 構造体を渡すと、SP_DEVINFO_DATA によって示されるデバイスに関連付けられているインターフェイスにのみ、列挙体が制限されます。

**Setupdienumdeviceinterfaces**は[**SP_DEVICE_INTERFACE_DATA**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_data)構造体を返します。 SP_DEVICE_INTERFACE_DATA には、インターフェイスの名前を取得するために使用できるエンコードされたフィールドを含む、インターフェイスクラスの GUID とインターフェイスに関するその他の情報が含まれています。 インターフェイス名を取得するには、次の手順を実行する必要があります。 [**Setupdigetdeviceinterfacedetail**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)を呼び出す必要があります。 **Setupdigetdeviceinterfacedetail**は、インターフェイスを定義するシステムオブジェクトツリー内のパスを含む[**SP_DEVICE_INTERFACE_DETAIL_DATA**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_detail_data_a)型の構造体を返します。
