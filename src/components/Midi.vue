<template>
  <div class='Midi'>
    {{midiDevices.inputs}}
    <div v-for='v in inputs'>
      <label>{{('000' + v.num).substr(-4)}}</label>
      <input v-bind:value='v.value' max='127' min='0' type='range' ></input>
    </div>
  </div>
</template>

<script>
export default{
  name: 'midi-control',
  data () {
    return {
      midiDevices: {
        inputs: {}
      },
      inputs: {}
    }
  },
  mounted: function () {
    let self = this
    ConnectMidiController()
    // controllerを紐付けるよ
    function ConnectMidiController () {
      // requestMIDIAccessはpromise型を返すのでthen()で成功した時と失敗した時の処理のコールバックを登録する
      navigator.requestMIDIAccess().then(requestSuccess, requestError)
    }
    function requestSuccess (data) {
      console.log('つながったよ', data)
      data.inputs.forEach(function (device) {
        // デバイス情報を保存
        self.midiDevices.inputs[device.name] = device
        // MIDIメッセージイベント受信したときの登録
        device.addEventListener('midimessage', inputEvent, false)
      })
    }
    // 入力が会ったときの処理
    function inputEvent (e) {
      self.inputs[e.data[1]] = {num: e.data[1], value: e.data[2]}
      console.log(self.inputs)
      self.$forceUpdate()
    }
    // エラーの時の処理
    function requestError (error) {
      console.error(error)
    }
  }
}
</script>
