---
title: PoolMon のスタートアップ コマンド
description: PoolMon を開始するには、コマンドラインで次の構文とパラメーターを使用してコマンドを入力します。
ms.assetid: 2aa0cf09-f016-46b9-af4e-0f3fbc6fbe5b
keywords:
- PoolMon スタートアップコマンドのドライバー開発ツール
topic_type:
- apiref
api_name:
- PoolMon Startup Command
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4c82c4c3d572ce7d5db2c4fa4d0da5936bc4fcb
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038076"
---
# <a name="poolmon-startup-command"></a>PoolMon のスタートアップ コマンド


PoolMon を開始するには、コマンドラインで次の構文とパラメーターを使用してコマンドを入力します。

```
    poolmon [/iTag] [/xTag] [/c [LocalTagFile]] [/g [PoolTagFile]] [/s[TSSessionID]] [ /p | /p /p ] [/e] [/( | /)]  [/t | /a| /f| /d | /b| /m] [/l] [/n [File]] [/? | /h] 
```

## <a name="span-idddk_poolmon_startup_command_toolsspanspan-idddk_poolmon_startup_command_toolsspanparameters"></a><span id="ddk_poolmon_startup_command_tools"></span><span id="DDK_POOLMON_STARTUP_COMMAND_TOOLS"></span>パラメータ


<span id="________i______"></span><span id="________I______"></span> **/i**   
指定されたプールタグを持つ割り当てのみを表示します。 PoolMon コマンドでは、複数の **/i**パラメーターを使用できます。 **/I**と*Tag*引数の間にスペースを入力しないでください。

<span id="________x______"></span><span id="________X______"></span> **/x**   
指定されたタグを持つ割り当てを表示から除外します。 PoolMon コマンドでは、複数の **/x**パラメーターを使用できます。 **/X**と*Tag*引数の間にスペースを入力しないでください。

<span id="_______Tag______"></span><span id="_______tag______"></span><span id="_______TAG______"></span>*タグ*   
プールタグまたはプールタグパターンを指定します。 プールタグでは大文字と小文字が区別されます。 *Tag*引数には、任意の文字の0個以上のインスタンスを表すアスタリスク ( **\*** )、または任意の文字の1つのインスタンスを表す疑問符 ( *<em>?</em>* ) を含めることができます。 アスタリスクを使用してタグを開始しないでください。

<span id="________c______"></span><span id="________C______"></span> **/c**   
各プールタグを使用するローカルコンピューター上のドライバーの一覧を表示する (マップされた\_ドライバー) に列を追加します。 この機能は、32ビットバージョンの Windows でのみサポートされています。

<span id="_______LocalTagFile______"></span><span id="_______localtagfile______"></span><span id="_______LOCALTAGFILE______"></span>*Localtagfile*   
ローカルタグファイルのパスとファイル名、ローカルコンピューター上のドライバーの一覧を含む書式設定されたテキストファイル、および割り当てられるタグ値を指定します。 このファイルは、 **/c**パラメーターを使用したときに表示される、マップされた\_ドライバー列のデータソースです。 既定値は localtag .txt です。

**/C**パラメーターを使用しても、 *localtagfile*の値を指定せず、poolmon によって現在のディレクトリにある localtag .txt ファイルが見つからない場合、poolmon はローカルコンピューターのドライバー (% SystemRoot%\\System32\\ドライバー\\\*) をスキャンして localtag .txt ファイルを生成します。

<span id="________g______"></span><span id="________G______"></span> **/g**   
Windows コンポーネントと、各タグを割り当てる一般的に使用されるドライバーの一覧を表示する (マップされた\_ドライバー) に列を追加します。

<span id="_______PoolTagFile______"></span><span id="_______pooltagfile______"></span><span id="_______POOLTAGFILE______"></span>*Pooltagfile*   
Windows コンポーネントおよび一般的に使用されるドライバーの名前と、割り当てられるタグ値を一覧表示する、書式設定されたテキストファイルのパスとファイル名を指定します。 このファイルは、 **/g**パラメーターを使用したときに表示される、マップされた\_ドライバー列のデータソースです。

既定値は、Microsoft によって提供されるファイルである pooltag .txt です。 *Pooltag .txt*は、Windows Driver KIT (WDK) の他のサブディレクトリのツール\\に含まれています。

<span id="________s______"></span><span id="________S______"></span> **/s**   
ターミナルサービスのセッションプールからの割り当てを表示します。

<span id="_______TSSessionID______"></span><span id="_______tssessionid______"></span><span id="_______TSSESSIONID______"></span>*Tssessionid*   
指定されたセッションプールからの割り当てのみを表示します。 **/S**パラメーターと*tssessionid*引数の間にスペースを入力しないでください。

<span id="________p______"></span><span id="________P______"></span> **/p**   
非ページプールからの割り当てのみを表示します。

<span id="________p__p_______"></span><span id="________P__P_______"></span> **/p/p**   
ページプールからの割り当てのみを表示します。

<span id="________e_______"></span><span id="________E_______"></span> **/e**   
プールの合計が表示されます。 合計がディスプレイの下部に表示されます。

<span id="__________or___"></span><span id="__________OR___"></span> **/(** または **/)**  
変更の並べ替えモードをオンにします。 **/(** または **/)** では、PoolMon は値ではなく値 (割り当て、解放された操作、およびバイト) の変更によって並べ替えます。 各値の変更は、値の後にかっこで囲まれて表示されます。

**/A**、 **/f**、 **/b** 、または **/m**と共に使用します。 たとえば、 **poolmon/a**を指定すると、ディスプレイが割り当ての数で並べ替えられます。**また、poolmon/(/a**は、割り当ての数の変化によって表示を並べ替えます。

左かっこと右かっこの文字は同じ効果を持ち、同義に使用できます。

<span id="________t______"></span><span id="________T______"></span> **/t**   
タグ名でアルファベット順に並べ替えます。 これが既定値です。

<span id="________a______"></span><span id="________A______"></span> **/a**   
割り当ての数でタグを並べ替えます。

<span id="________f_______"></span><span id="________F_______"></span> **/f**   
タグを無料操作の数で並べ替えます。

<span id="________d______"></span><span id="________D______"></span> **/d**   
バイト割り当てと解放されたバイト数の違いによってタグを並べ替えます。

<span id="________b_______"></span><span id="________B_______"></span> **/b**   
使用されたバイト数でタグを並べ替えます。

<span id="________m_______"></span><span id="________M_______"></span> **/m**   
タグを割り当てごとにバイト単位で並べ替えます。

<span id="________l______"></span><span id="________L______"></span> **/l**   
強調表示をオンにします。 既定では、前回の更新以降に変更された値が、PoolMon によって強調表示されます。

<span id="________n______"></span><span id="________N______"></span> **/n**   
コマンドウィンドウに表示するのではなく、PoolMon 出力のスナップショットをファイルに保存します。 他のコマンドラインパラメーターを含めて、出力を構成できます。

スナップショットデータは静的であるため、PoolMon の値の変化を示す列はスナップショットファイルに表示されません。

<span id="_______File______"></span><span id="_______file______"></span><span id="_______FILE______"></span>*ファイル*   
スナップショットファイルの名前と場所を指定します。 既定値は poolsnap .log です。

<span id="__________or__h"></span><span id="__________OR__H"></span> **/?** または **/h**  
コマンドライン構文を表示します。 **/?** および **/h**パラメーターは同じ効果を持ち、同義に使用できます。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

PoolMon は、64ビット版の Windows Server 2003 で localtag .txt ファイルを生成することはできません。 その結果、 **/c**パラメーターとその機能は、32ビットバージョンの Windows でのみ使用できます。

**/C**パラメーターと **/g**パラメーターを同じコマンドで使用できます。 この操作を行うと、[マップされた\_ドライバー] 列に、ローカルのタグファイルとプールタグファイルの両方のデータが表示されます。

**/C**および **/g**を使用して、[マップされた\_ドライバー] 列にある他のファイルのデータを表示することもできます。そのためには、-- **poolmon/c** *filename*または**poolcom/g** *filename*のいずれかのパラメーターを指定してファイル名と場所を指定します。 この場合、 **/c**パラメーターと **/g**パラメーターは同じように動作し、同義に使用できます。

ターミナルサービスセッションプールの監視は、Windows Server 2003 以降のバージョンの Windows でのみ使用できます。

Win32 サブシステムのカーネルモード部分は、コンピューターがターミナルサーバーとして構成されている場合にのみ、ターミナルサービスのセッションプールからメモリを割り当てます。 それ以外の場合は、Windows によって、システムプールからターミナルサービスのプールメモリが割り当てられます。









