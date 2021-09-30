<template>
  <div class="rage-box">
    <input class="input" placeholder="Type something (e.g EZ JG)" v-model="input" @input="InputChanged(input)" />
    
		<p class="warning"> {{ warning }}</p>

		<p class="display" title="This is how it will look lik in the LoL chat !" v-html="display"></p>
		<img src="../assets/copy.png" class="copy" @click="CopyText" title="Copy Text">
		<p class="note">This is how the text will show in the chat.</p>
		<p class="note">Please notice that this only works in the lobby chat, and doesn't work in-game !</p>
    
		<img src="../assets/copy.png" class="copy2" @click="CopyText" title="Copy Text">
  </div>
</template>

<script>
import Fonts from '../helpers/fonts.js'

export default {
  name: 'RageBox',

  data: () => {
    return {
      input: '',
      display: '',
      warning: '',
      letters: Fonts['big font']
    }
  },

  mounted: function () {
    this.InputChanged('EZ JG')
  },

  methods: {
    InputChanged: function (input) {
      var text = input.toUpperCase()

      var lines = [
        '░',
        '░',
        '░'
      ];

      for (var i = 0; i < text.length; i++) {
        var letter = text.charAt(i)

        if (!(letter in this.letters)) {
          this.warning = "One or more characters are not supported !"
          return false
        }

        var l = this.letters[letter].split('|')

        lines[0] += l[0] + '░'
        lines[1] += l[1] + '░'
        lines[2] += l[2] + '░'
      }

      if (lines[0].length > 31) {
        this.warning = 'The number of characters is too much for the LoL Chat size !!'
      } else {
        this.warning = ''
      }

      var emptyLine = '░'.repeat(lines[0].length)


      this.display = emptyLine + '<br>' + lines[0] + '<br>' + lines[1] + '<br>' + lines[2] + '<br>' + emptyLine
    },

    CopyText: function () {
      var input = document.createElement('textarea');
      var brRegex = /<br\s*[/]?>/gi;
      input.innerHTML = ".\r\n" + this.display.replace(brRegex, "\r\n")

      document.body.appendChild(input);

      input.select();

      document.execCommand('copy');
      document.body.removeChild(input);
    }
  }
}
</script>

<style scoped>
  .rage-box {
    text-align: center;
  }

  .input {
    display: block;
    margin: 50px auto 0px auto;
    width: 380px;
    height: 40px;
    background-color: rgba(0, 0, 0, 0.5);
    border: 1px solid #665426;
    color: white;
    font-size: 20px;
    padding: 3px 15px 3px 15px;
    text-align: center;
  }

  .input:focus {
    outline: none;
    border: 1px solid #a78739;
  }

  .display {
    padding: 20px;
    color: white;
    display: block;
    width: 350px;
    height: 160px;
    margin: 20px auto;
    background-color: rgba(0, 0, 0, 0.5);
    border: 1px solid #665426;
    text-align: center;
  }

  .copy {
    display: inline-block;
    width: 32px;
    position: relative;
    margin-top: 0px;
    top: -65px;
    left: 165px;
    cursor: pointer;
  }

  .copy2 {
    display: none;
    width: 32px;
    margin-top: 0px;
    cursor: pointer;
  }

  .warning {
    color: rgb(255, 91, 91);
    font-size: 16px;
    text-align: center;
    margin-top: 5px;
  }

  .note {
    color: #e9bf57;
    margin: 5px;
  }

  
  @media only screen and (max-width: 450px) {
    .copy {
      display: none;
    }

    .input {
      width: 80%;
    }

    .display {
      width: 80%;
    }

    .copy2 {
      display: inline-block;
    }
  }

</style>
