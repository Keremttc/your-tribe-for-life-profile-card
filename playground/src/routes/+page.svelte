<script>
    let { data } = $props(); 
    const member = data.member;
</script>

<section class="outlay">
    <section class="mycard-front mycard-style">
        <div>
           <img src={member?.avatar} alt={member?.name}>
        </div>    
        <h1>{member?.name}</h1>
    </section>

    <section class="mycard-back mycard-style">
        <p>{member?.bio}</p>
    </section>
</section>

