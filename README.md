
# Alguns codigos salvos
## Wordpress em geral


# WP_Query

## Args

**1) Args**

     <?php
        	$args = array(
        		'post_type' => 'name',
        		'posts_per_page' => -1
        	);
        	$the_query = new WP_Query($args);
        ?>
**2)Args taxonomy**

    <?php
    	$args = array(
    		'post_type' => 'name',
    		'posts_per_page' => -1,
    		'tax_query' => array(
    			array (
    			'taxonomy' => 'taxonomy_name',
    			'field' => 'slug',
    			'terms' => $categoria,
    			)
    		),
    	);
    ?>
**3)**

    'paged' => $paged,

## Query

    <?php if ($the_query->have_posts()): ?>
    	<?php while ($the_query->have_posts()) : $the_query->the_post() ?>
    
    			    //content
    
    	<?php endwhile;  wp_reset_postdata(); ?>
    <?php endif; ?>

# Pagination

## Inicio

   <?php 
        global $wp_query;
        $wp_query->query_vars['paged'] > 1 ? $current = $wp_query->query_vars['paged'] : $current = 1;
        $big = 999999999;
    ?>


## Adicionar nos args

    'paged' => $paged,

--------------------------

## Conteudo

   	<div class="pagination">
		<?php
			echo paginate_links( array(
			'format'  => 'page/%#%',
			'current' => $current,
			'total'   => $the_query->max_num_pages,
			'show_all' => true,
			'prev_next' => true,
			'prev_text' => false,
			'next_text' => false,
			'type' => 'list',
		) );
		?>	
	</div>
    
# Search

    <?php 
        $busca = $_GET['busca'];
        if ($busca){
    ?>
    
    
    <?php if ($the_query->have_posts()) : ?>
    	<?php while ($the_query->have_posts()) : $the_query->the_post() ?>
            <?php 
                $busca = strtoupper($busca); 
                $titulo = strtoupper(get_the_title());
                if(strpos($titulo, $busca) !== false):
            ?>
    
            //Adicionar conteudo aqui
    
        <?php endwhile;>
    <?php endif;>
    
    <?php }?>

> ***O que ele faz? Verifica se da um match entre o titulo e o conteudo do input para aparecer na página. Colocar uma Query normal como else
> no fim do ultimo php para carregar a página normalmente Para caso não
> tenha sido enviado um get ou post de busca.***

# Category filter

    <?php 
        $busca = $_POST['categoria'];
        if ($categoria){
    ?>
    
    <?php
    	$args = array(
    		'post_type' => 'name',
    		'posts_per_page' => -1,
    		'tax_query' => array(
    			array (
    			'taxonomy' => 'taxonomy_name',
    			'field' => 'slug',
    			'terms' => $categoria,
    			)
    		),
    	);
    ?>
    
    
    <?php if ($the_query->have_posts()): ?>
    	<?php while ($the_query->have_posts()) : $the_query->the_post() ?>
    
    			    //Do it
    
    	<?php endwhile;  wp_reset_postdata(); ?>
    <?php endif; ?>
    
    
    <?php }?>


> ***Colocar uma Query normal como else no fim do ultimo php para carregar a página normalmente Para caso não tenha sido enviado um get
> ou post de categoria.***

# Mostrar todos os terms de uma determinada taxonomia

     <?php 
        $terms = get_terms( 'taxonomy', array(
            'hide_empty' => false,
        ) );
        foreach ($terms as $terms) {
            echo '<li id="'.$terms->slug.'"class="categoria">'.$terms->name.'</li>';
        }
    ?>

# Mostrar os terms de uma taxonomia de um post

    <?php $cats = get_the_terms(get_the_ID(), 'taxonomy_name');?>
        <?php foreach( $cats as $cat): ?>
    
            echo '<li id="'.$cats->slug.'">'.$cats->name.'</li>';
    
        <?php endforeach; ?>

# Mostrar as tags de um post

    $tags = get_the_tags(get_the_ID());
    foreach ($tags as $tags) {
        echo '<li>'.$tags->name.'</li>';
    }
    
# Field relacional

    <?php $posts = get_field('field') ?>
        <?php foreach( $posts as $post):?>
            <?php setup_postdata($post); ?>
    
            //Conteudo
    
        <?php endforeach; ?>
---

# Meus Snippets Vscode



HTML
-------------------------------------------

{
	// Place your snippets for html here. Each snippet is defined under a snippet name and has a prefix, body and 
	// deion. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
	// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
	// same ids are connected.
	// Example:
	// "Print to console": {
	// 	"prefix": "log",
	// 	"body": [
	// 		"console.log('$1');",
	// 		"$2"
	// 	],
	// 	"deion": "Log output to console"
	// }
	"PHP tag": {
        "prefix": "php",
        "body": [
            "<?php $1 ?>"
        ],
        "deion": "Insert php tags"
	},
	"the field WordPress": {
		"prefix": ["tf"],
		"body": ["<?php the_field('${1:field_name}'); ?>"],
		"deion" : "A field call."
	},
	"the sub field WordPress": {
		"prefix": ["ts"],
		"body": ["<?php the_sub_field('${1:field_name}'); ?>"],
		"deion" : "A sub field call."
	},
	"repeater WordPress": {
		"prefix": ["repeater"],
		"body": ["<?php if (have_rows('repeater_field_name')) : ?>","\t","<?php while (have_rows('repeater_field_name')) : the_row(); ?>","\t","${1}","\t","<?php endwhile; ?>","\t","<?php endif;  ?>"],
		"deion" : "A repeater call."
	},
	"get template directory WordPress": {
		"prefix": ["get_template_directory"],
		"body": ["<?php echo get_template_directory_uri(); ?>"],
		"deion" : "Get template directory."
	},
	"get home WordPress": {
		"prefix": ["get_home"],
		"body": ["<?php echo get_home_url(); ?>"],
		"deion" : "Get home."
	}
}


CSS
-------------------------------------------

{
	// Place your snippets for css here. Each snippet is defined under a snippet name and has a prefix, body and 
	// deion. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
	// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
	// same ids are connected.
	// Example:
	// "Print to console": {
	// 	"prefix": "log",
	// 	"body": [
	// 		"console.log('$1');",
	// 		"$2"
	// 	],
	// 	"deion": "Log output to console"
	// }
	"media": {
		"prefix": "media(){}",
		"body": [
		  "@media (max-width: ${1|1200|}px) {",
			
"}"
	
],
		"deion": "Media"
	  }
	
}
