<script>
  export let onClose;
</script>

<div class="popup">
  <div class="window" style="width: 300px;">
    <div class="title-bar">
      <div class="title-bar-text">About</div>
      <div class="title-bar-controls">
        <button aria-label="Close" on:click={onClose}></button>
      </div>
    </div>
    <div class="window-body">
      <div class="content">
        <p>
          For the children of the 90s, the internet was a revolutionary force
          that changed our lives forever. It opened up new worlds of
          information, communication, and entertainment that were previously
          unimaginable. We were the first generation to grow up with the
          internet, and it has shaped who we are today.
        </p>
        <p>
          The internet gave us access to a vast amount of knowledge at our
          fingertips. We could explore different cultures, learn new skills, and
          stay informed about global events. It also allowed us to connect with
          people from all over the world, making it easier to maintain
          friendships and build new ones.
        </p>
        <p>
          For many of us, the internet was a place of creativity and
          self-expression. We built our own websites, shared our thoughts on
          blogs, and created content that could reach a global audience. It was
          a time of experimentation and discovery, and it fostered a sense of
          community and collaboration.
        </p>
        <p>
          Today, the internet continues to influence our lives in profound ways.
          It has reshaped industries, transformed the way we work and
          communicate, and created new opportunities for innovation. However, it
          has also brought challenges, such as information overload and concerns
          about privacy.
        </p>
        <p>
          Despite these challenges, the spirit of the 90s internet lives on in
          those of us who experienced its early days. We cherish the sense of
          wonder and possibility that it brought, and we strive to keep that
          spirit alive in a world that is increasingly connected. We believe in
          the power of the internet to bring people together, inspire
          creativity, and make the world a better place.
        </p>
      </div>
      <button class="button" on:click={onClose}>Close</button>
    </div>
  </div>
</div>

<style>
  .popup {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .window {
    border: 2px solid #000;
    background: #c0c0c0;
    box-shadow: 5px 5px 0 #0000006e;
    max-height: 90%; /* Begrenze die maximale Höhe des Fensters */
  }

  .title-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #000080;
    color: #fff;
    padding: 2px 5px;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
  }

  .title-bar-text {
    font-weight: bold;
  }

  .title-bar-controls button {
    background: #c0c0c0;
    border: none;
    width: 16px;
    height: 16px;
    padding: 0;
    margin: 0 2px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }

  .title-bar-controls button::before {
    content: "×";
    font-size: 14px;
    line-height: 1;
  }

  .window-body {
    padding: 10px;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
    overflow: auto; /* Ermöglicht das Scrollen, wenn der Inhalt zu groß ist */
  }

  .content {
    max-height: 70vh; /* Begrenze die maximale Höhe des Inhalts */
    overflow-y: auto; /* Ermöglicht vertikales Scrollen */
  }

  .button {
    background: #c0c0c0;
    border: 2px solid #000;
    padding: 2px 10px;
    cursor: pointer;
    font-family: "Microsoft Sans Serif", sans-serif;
    font-size: 12px;
    margin-top: 10px;
  }

  .button:active {
    box-shadow: inset 2px 2px 0 #000;
  }
</style>
