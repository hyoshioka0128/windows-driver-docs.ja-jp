---
title: USB I/O ターゲットによるファイルの作成
description: USB I/O ターゲットによるファイルの作成
ms.assetid: 44bbc4c7-632d-4d75-94b9-f65e4d480e90
keywords:
- ユーザーモードドライバー WDK UMDF、USB i/o ターゲット、ファイル作成
- UMDF WDK、USB i/o ターゲット、ファイル作成
- ユーザーモードドライバーフレームワーク WDK、USB i/o ターゲット
- フレームワークベースのドライバー WDK UMDF、USB i/o ターゲット
- USB i/o ターゲット WDK UMDF、ファイル作成
- I/o ターゲット WDK UMDF、USB、ファイル作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3b35160aaba1c34d7fcfa9c70c3849247bb78fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843189"
---
# <a name="file-creation-by-a-usb-io-target"></a>USB I/O ターゲットによるファイルの作成


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

USB i/o ターゲットは、初期化中に、スタック内のファイルオブジェクトを作成します。このオブジェクトは、USB i/o ターゲットが開いたままにする既定のセッションを表します。 スタック内のファイルオブジェクトの詳細については、「 [i/o を処理するためのファイルオブジェクトの作成](creating-a-file-object-to-handle-i-o.md)」を参照してください。 USB i/o ターゲットまたはその USB パイプターゲットの子は、このファイルオブジェクトを使用して、発生した i/o (たとえば、USB 構成記述子を取得するための i/o) を送信します。

ドライバーは、このスタック内のファイルオブジェクトをフォーマット関数で使用できます (たとえば、ドライバーがに i/o を送信する必要がある場合、このファイルオブジェクトへのポインターを[**Iwdfiotarget:: FormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)メソッドの呼び出しで*pFile*パラメーターに渡すことができます)。このファイルオブジェクトの既定のセッション。 スタック内のファイルオブジェクトを取得するために、ドライバーは[**Iwdfiotarget:: GetTargetFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-gettargetfile)メソッドを呼び出すことができます。

このスタック内のファイルオブジェクトは、ドライバーが i/o ターゲットで[**Iwdfobject::D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)メソッドを呼び出したとき、または i/o ターゲットの親が破棄されたときに暗黙的に呼び出されたときに、i/o ターゲットが明示的に破棄されると閉じられます。

デバイスの削除時に、このスタック内のファイルオブジェクトの i/o が未処理のままである場合、このファイルオブジェクトは閉じることができず、UMDF はドライバーの停止を生成します。 詳細については、「[ドライバーによって作成されたファイルオブジェクトの作成と使用](creating-and-using-driver-created-file-objects.md)」を参照してください。

 

 





