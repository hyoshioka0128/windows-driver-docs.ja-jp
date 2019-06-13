---
title: I/O 要求パケット
description: I/O 要求パケット
ms.assetid: 72288D9A-86F7-4145-8470-FFA1AC26E9BF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62ea0c35c6e7c36e8a08782fa03434cede2e7cbb
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63371285"
---
# <a name="io-request-packets"></a>I/O 要求パケット


デバイス ドライバーに送信される要求のほとんどは、I/O 要求パケット ([**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)) にパッケージ化されます。 オペレーティング システムのコンポーネントまたはドライバーが、[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336) を呼び出すことにより、ドライバーに IRP を送信します。IoCallDriver には、[**DEVICE\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff543147) へのポインターと **IRP** へのポインターを指定する 2 つのパラメーターがあります。 **DEVICE\_OBJECT** には、関連付けられている [**DRIVER\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff544174) に対するポインターがあります。 コンポーネントから **IoCallDriver** が呼び出されると、コンポーネントが "*IRP をデバイス オブジェクトに送信する*"、"*IRP をデバイス オブジェクトに関連付けられたドライバーに送信する*"、などの表現を使うことがあります。 また、*IRP を送信する*、という言い方の代わりに *IRP を渡す*や *IRP を転送する*、などの言い方をする場合もあります。

通常、IRP は、1 つのスタック上に配置されたいくつかのドライバーによって処理されます。 スタック上の各ドライバーは、それぞれ個別のデバイス オブジェクトに関連付けられます。 詳しくは、「[デバイス ノードとデバイス スタック](device-nodes-and-device-stacks.md)」をご覧ください。 [  **IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694) がデバイス スタックにより処理されると、通常、**IRP** はまずデバイス スタックの最上段にあるデバイス オブジェクトに送信されます。 たとえば、次の図のように、**IRP** がデバイス スタックによって処理されると、IRP は、デバイス スタックの最上段にあるフィルター デバイス オブジェクト (Filter DO) に送信されます。

![デバイス ノードとデバイス スタックの図](images/prosewaredevicenode03.png)

## <a name="span-idpassinganirpdownthedevicestackspanspan-idpassinganirpdownthedevicestackspanspan-idpassinganirpdownthedevicestackspanpassing-an-irp-down-the-device-stack"></a><span id="Passing_an_IRP_down_the_device_stack"></span><span id="passing_an_irp_down_the_device_stack"></span><span id="PASSING_AN_IRP_DOWN_THE_DEVICE_STACK"></span>下のデバイス スタックへの IRP の受け渡し


I/O マネージャーが、図に示す Filter DO に IRP を送信する例を考えてみましょう。 Filter DO に関連付けられたドライバー、AfterThought.sys は IRP を処理した後、デバイス スタックで 1 つ下にあるデバイス オブジェクトであるファンクショナル デバイス オブジェクト (FDO) に IRP を渡します。 ドライバーがデバイス スタックで 1 つ下のデバイス オブジェクトに IRP を渡すことを*下のデバイス スタックに IRP を渡す*、と表現します。

IRP によっては、デバイス スタックを下降して、物理デバイス オブジェクト (PDO) にまで送信されるものもあります。 また、PDO よりも上にあるいずれかのドライバーで処理されるため、PDO には到達しない IRP もあります。

## <a name="span-idirpsareself-containedspanspan-idirpsareself-containedspanspan-idirpsareself-containedspanirps-are-self-contained"></a><span id="IRPs_are_self-contained"></span><span id="irps_are_self-contained"></span><span id="IRPS_ARE_SELF-CONTAINED"></span>自己完結型の IRP


IRP の構造は、ドライバーが I/O 要求を処理するのに必要な情報をすべて保持しているという意味で自己完結型であるといえます。 IRP の構造には、スタック中で関与するすべてのドライバーに共通する情報を保持する部分があります。 また IRP には、スタック上の特定のドライバーに固有の情報を保持する部分もあります。

 

 





