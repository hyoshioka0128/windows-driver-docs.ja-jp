---
title: デバイスが接続されているかどうかの判断
description: デバイスが接続されているかどうかの判断
ms.assetid: 26dc3c2b-49a6-4bba-b86b-2c93a1914f87
keywords:
- 接続されていないデバイスを再インストールします。
- 接続されていないデバイスの再インストール WDK
- デバイスの電源接続時のチェック
- デバイスの電源接続時の確認
- デバイスのチェック WDK で接続されています。
- WDK のデバイスで接続を決定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa9d278f6b4d44cfff671b4f510bdf187b92984b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346196"
---
# <a name="determining-whether-a-device-is-plugged-in"></a>デバイスが接続されているかどうかの判断


注意してくださいを自動起動の動作*デバイス インストール アプリケーション*のハードウェアでユーザーをかどうかは最初に依存する必要がありますまたは最初に、配布メディアを挿入します。 独立系ハードウェア ベンダー (Ihv) は、通常、1 つの配布のディスクを提供し、ディスクでは、1 つの自動起動アプリケーションしか、ため、デバイスの自動起動のインストール アプリケーションは、デバイスが接続されているかどうかを決定する必要があります。

デバイスが接続されているかどうかを判断する、アプリケーションを呼び出すことができます、 [ **UpdateDriverForPlugAndPlayDevices** ](https://msdn.microsoft.com/library/windows/hardware/ff553534)関数は、デバイスのハードウェア ID を渡します。 次のいずれかが true の場合、デバイスを接続します。

-   関数を返します**TRUE**します。 (これもインストール、デバイスのドライバーです。)

-   関数を返します**FALSE**と Win32 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)ERROR_NO_MORE_ITEMS を返します。 (インストールは行われません。)

デバイスが接続されていない場合は、関数を返します**FALSE**と[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) NO_SUCH_DEVINST を返します。 (インストールは行われません。)

### <a name="reinstalling-an-unplugged-device"></a>接続されていないデバイスを再インストールします。

抜かれて以前接続されていたデバイスのようになりましたが場合、デバイスの*devnode*は非アクティブと非表示の両方が、システムのままになります。 このようなデバイスを再インストールすることができます、前に最初この「ファントム」の devnode を検索して再インストールを必要とするマークを付けます。 戻り、デバイスが接続されている、ときにプラグ アンド プレイがデバイスを再列挙の新しいドライバーを検索し、デバイスのドライバーをインストールします。

**接続されていないデバイスを再インストールします。**

1.  呼び出す、 [SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=98735)関数。

    [SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=194252)関数により、正しい INF ファイルに存在するが、 *%systemroot%\\inf*ディレクトリ。

2.  接続されていないデバイスを検索します。

    呼び出す、 [ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)関数。 この関数の呼び出しで DIGCF_PRESENT フラグのクリア、*フラグ*パラメーター。 検索する必要がある*すべて*が存在するものだけでなく、デバイス。 内の特定のデバイス クラスを指定することで、検索の結果を絞り込むことができます、 *ClassGuid*パラメーター。

3.  ハードウェア Id と接続されていないデバイスの互換性 Id を検索します。

    **SetupDiGetClassDevs**を識別するハンドルを返します、[デバイス情報設定されている](device-information-sets.md)または (最初の手順では、デバイス クラスを指定したことを想定) デバイス クラスではなく、接続されているかどうか、インストールされているすべてのデバイスを含むです。 連続した呼び出しによって、 [ **SetupDiEnumDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff551010)関数の場合、デバイスの情報セット内のすべてのデバイスを列挙するためにこのハンドルを使用することができます。 各呼び出しは、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)デバイスの構造体。 ハードウェア Id の一覧を取得する呼び出し、 [ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967)関数と、*プロパティ*パラメーター SPDRP_HARDWAREID に設定します。 互換性 Id の一覧を取得するには、同じ関数を呼び出しますが、*プロパティ*パラメーター SPDRP_COMPATIBLEIDS に設定します。 両方の一覧は、マルチ SZ 文字列です。

4.  デバイスと、ハードウェア Id (または互換性 Id) の前の手順の ID の間で一致を検索します。

    デバイスのハードウェア ID または互換性のある ID と ID の完全な文字列比較を実行することを確認します。 部分的な比較は、間違った一致する可能性があります。

    一致を検索するときに呼び出す、 [ **CM_Get_DevNode_Status** ](https://msdn.microsoft.com/library/windows/hardware/ff538514)関数を SP_DRVINFO_DATA **。DevInst**で、 *dnDevInst*パラメーター。 デバイスが接続されていないことを確認 CR_NO_SUCH_DEVINST がこの関数に返される場合 (つまり、ファントム devnode が)。

5.  デバイスをマークします。

    呼び出す、 [ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967)関数と、*プロパティ*パラメーター SPDRP_CONFIGFLAGS に設定します。 この関数が戻るとき、 *PropertyBuffer*パラメーターが、デバイスの指す**ConfigFlags**レジストリからの値。 CONFIGFLAG_REINSTALL でこの値のビットごとの OR を実行 (で定義されている*Regstr.h*)。 これを行う呼び出し、 [ **SetupDiSetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552169)関数で、*プロパティ*SPDRP_CONFIGFLAGS に設定するパラメーター、 *PropertyBuffer* 、デバイスのアドレスに設定するパラメーターの変更**ConfigFlags**値のこの操作の変更、レジストリの**ConfigFlags**を組み込む値、CONFIGFLAG_REINSTALL フラグです。 これにより、次回デバイスが再度列挙したときに再インストールするデバイスです。

6.  デバイスを接続します。

    プラグ アンド プレイはデバイスを再列挙の新しいドライバーを検索し、そのドライバーをインストールします。

 

 





