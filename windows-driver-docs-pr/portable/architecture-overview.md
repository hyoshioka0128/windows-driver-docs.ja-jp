---
Description: Architecture overview of Windows portable devices
title: アーキテクチャの概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c788eed2e620d9c9e940d718f1fa09d78a06d3ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572158"
---
# <a name="architecture-overview"></a>アーキテクチャの概要


WPD アーキテクチャは、3 つのプロセスに分割できます。 これらのプロセス内では WPD の 3 つの主要コンポーネント: API、シリアライザー、およびドライバー。 次の図は、これらのプロセスと WPD アーキテクチャを構成するコンポーネントを示しています。

![wpd を構成する 3 つのプロセス](images/wpd_overview_figure1.png)

## <a name="span-idthewpdapplicationprogramminginterfacespanspan-idthewpdapplicationprogramminginterfacespanspan-idthewpdapplicationprogramminginterfacespanthe-wpd-application-programming-interface"></a><span id="The_WPD_Application_Programming_Interface"></span><span id="the_wpd_application_programming_interface"></span><span id="THE_WPD_APPLICATION_PROGRAMMING_INTERFACE"></span>WPD アプリケーション プログラミング インターフェイス


WPD API は、インプロセス COM サーバーとして実装されます。 API では、標準の Microsoft Win32 Api を使用して、適切な WPD ドライバーと通信します。 WPD シリアライザーと呼ばれるコンポーネントは、パックまたはまたは Windows Driver Frameworks (WDF) - ユーザー モード ドライバー フレームワーク (UMDF) バッファーからパラメーターを展開する API のオブジェクトと、ドライバーの両方で使用されます。

## <a name="span-idthewpdserializerspanspan-idthewpdserializerspanspan-idthewpdserializerspanthe-wpd-serializer"></a><span id="The_WPD_Serializer"></span><span id="the_wpd_serializer"></span><span id="THE_WPD_SERIALIZER"></span>WPD シリアライザー


WPD シリアライザーは、インプロセス COM サーバーとしても実装されます。 WPD API では、シリアライザーを使用して、コマンドとパラメーターをドライバーに送信されるメッセージ バッファーにパックします。 ドライバーは、処理のためのこれらのメッセージ バッファーをアンパックするのには、シリアライザーを使用します。 ドライバーは、WPD API に返される応答バッファーにデータとパラメーターをパックするシリアライザーを使用し、WPD API はこれらの呼び出し元に、結果を返す応答のバッファーをアンパックするのには、シリアライザーを使用します。

## <a name="span-idwpddriverspanspan-idwpddriverspanspan-idwpddriverspanwpd-driver"></a><span id="WPD_Driver"></span><span id="wpd_driver"></span><span id="WPD_DRIVER"></span>WPD ドライバー


WPD ドライバーは、標準の Windows Driver Frameworks (WDF) - ユーザー モード ドライバー フレームワーク (UMDF) ドライバーとして実装されます。 WPD ドライバーは、ドライバーのホストと呼ばれる別のプロセスで WUDF によってホストされます。

ドライバー (これは表示されません図では、バッファーを受信する方法は、ドライバーに重要でないため WUDF reflector からメッセージを受信します。 詳細については WUDF ドキュメントを参照)。 ドライバーは、WPD API によって受信された WPD メッセージを処理するための WPD に固有の IOCTL ハンドラーを実装します。 ドライバーは、コマンドとこれらのメッセージ バッファーからパラメーターをアンパックして、応答をバッファーにパックする WPD シリアライザーを使用します。

WPD ドライバーは、自分のデバイスで (CreateFile、ReadFile、WriteFile など) などの Win32 ファイル操作を使用して通常アクセス、カーネル モード ドライバーを経由して通信できます。 共通のバスでは、Microsoft はこれをユーザー モードのみのドライバー ソリューションを出荷するベンダーを使用する仕入先の標準のカーネル ドライバーを提供します。

 

 




